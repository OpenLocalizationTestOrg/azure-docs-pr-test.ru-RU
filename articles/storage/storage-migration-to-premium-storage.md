---
title: "виртуальные машины aaaMigrating tooAzure хранилище Premium | Документы Microsoft"
description: "Перенос в существующие виртуальные машины tooAzure хранилище Premium. Хранилище Premium обеспечивает поддержку дисков с высокой производительностью и малой задержкой для интенсивных рабочих нагрузок ввода-вывода на виртуальных машинах Azure."
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
ms.openlocfilehash: cd812bdbe39f43fe053a998d96788045d5a43258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a><span data-ttu-id="f2165-104">Миграция tooAzure хранилище Premium (неуправляемой диски)</span><span class="sxs-lookup"><span data-stu-id="f2165-104">Migrating tooAzure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="f2165-105">В этой статье рассматриваются как toomigrate виртуальной Машины, которая использует tooa неуправляемые стандартные диски виртуальной Машины, использующей неуправляемого диски premium.</span><span class="sxs-lookup"><span data-stu-id="f2165-105">This article discusses how toomigrate a VM that uses unmanaged standard disks tooa VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="f2165-106">Рекомендуется использовать диски управляемых Azure для новых виртуальных машин и преобразовании предыдущих дисков toomanaged неуправляемые дисков.</span><span class="sxs-lookup"><span data-stu-id="f2165-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="f2165-107">Управляемые диски дескриптор hello базового хранилища счетов, не нужно.</span><span class="sxs-lookup"><span data-stu-id="f2165-107">Managed Disks handle hello underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="f2165-108">Дополнительные сведения см. в статье [Managed Disks Overview](storage-managed-disks-overview.md) (Обзор Управляемых дисков).</span><span class="sxs-lookup"><span data-stu-id="f2165-108">For more information, please see our [Managed Disks Overview](storage-managed-disks-overview.md).</span></span>
>

<span data-ttu-id="f2165-109">Хранилище Azure Premium обеспечивает поддержку дисков с высокой производительностью и малой задержкой для виртуальных машин с интенсивной рабочей нагрузкой ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="f2165-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="f2165-110">Путем переноса приложения в виртуальной Машине диски tooAzure хранилище Premium, могут пользоваться преимуществами hello скорости и производительность этих дисков.</span><span class="sxs-lookup"><span data-stu-id="f2165-110">You can take advantage of hello speed and performance of these disks by migrating your application's VM disks tooAzure Premium Storage.</span></span>

<span data-ttu-id="f2165-111">в этом руководстве Hello задачей является новым пользователям toohelp хранилища Azure Premium лучше подготовить toomake плавный переход от их текущего tooPremium системы хранения.</span><span class="sxs-lookup"><span data-stu-id="f2165-111">hello purpose of this guide is toohelp new users of Azure Premium Storage better prepare toomake a smooth transition from their current system tooPremium Storage.</span></span> <span data-ttu-id="f2165-112">Hello руководстве рассматриваются три основные компоненты hello в этом процессе:</span><span class="sxs-lookup"><span data-stu-id="f2165-112">hello guide addresses three of hello key components in this process:</span></span>

* [<span data-ttu-id="f2165-113">Планирование миграции hello tooPremium хранилища</span><span class="sxs-lookup"><span data-stu-id="f2165-113">Plan for hello Migration tooPremium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="f2165-114">Подготовка и копирования виртуальные жесткие диски (VHD) tooPremium хранилища</span><span class="sxs-lookup"><span data-stu-id="f2165-114">Prepare and Copy Virtual Hard Disks (VHDs) tooPremium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* <span data-ttu-id="f2165-115">[создание виртуальной машины Azure c использованием хранилища класса Premium](#create-azure-virtual-machine-using-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="f2165-115">[Create Azure Virtual Machine using Premium Storage](#create-azure-virtual-machine-using-premium-storage)</span></span>

<span data-ttu-id="f2165-116">Можно перенести виртуальные машины из других платформ tooAzure хранилище Premium или переноса существующих виртуальных машин Azure из стандартного хранилища tooPremium хранилища.</span><span class="sxs-lookup"><span data-stu-id="f2165-116">You can either migrate VMs from other platforms tooAzure Premium Storage or migrate existing Azure VMs from Standard Storage tooPremium Storage.</span></span> <span data-ttu-id="f2165-117">В этом руководстве рассматриваются оба этих сценария.</span><span class="sxs-lookup"><span data-stu-id="f2165-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="f2165-118">Выполните действия hello, указанный в hello соответствующий подраздел в зависимости от вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="f2165-118">Follow hello steps specified in hello relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="f2165-119">Общие сведения о возможностях хранилища класса Premium и ценах на него см. в статье [Хранилище класса «Премиум»: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f2165-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="f2165-120">Мы рекомендуем перейти любого диска виртуальной машины, требуя высокой tooAzure операций ввода-ВЫВОДА хранилища Premium для hello наилучшей производительности для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f2165-120">We recommend migrating any virtual machine disk requiring high IOPS tooAzure Premium Storage for hello best performance for your application.</span></span> <span data-ttu-id="f2165-121">Если диск не требует большого числа операций ввода-вывода в секунду, выберите более доступное хранилище уровня Standard — в этом случае данные с диска виртуальной машины будут храниться не на твердотельных, а на жестких дисках.</span><span class="sxs-lookup"><span data-stu-id="f2165-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="f2165-122">Завершение процесса миграции hello в полном объеме может потребоваться дополнительные действия до и после hello шаги, описанные в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="f2165-122">Completing hello migration process in its entirety may require additional actions both before and after hello steps provided in this guide.</span></span> <span data-ttu-id="f2165-123">Примеры включают настройку виртуальных сетей или конечные точки или внесения изменений в код приложения hello сам которого может потребоваться некоторое время простоя в приложении.</span><span class="sxs-lookup"><span data-stu-id="f2165-123">Examples include configuring virtual networks or endpoints or making code changes within hello application itself which may require some downtime in your application.</span></span> <span data-ttu-id="f2165-124">Эти действия являются уникальными tooeach приложения и они должны выполняться вместе с hello шаги, описанные в этом руководство по toomake hello полного перехода tooPremium хранилища, как можно менее заметным.</span><span class="sxs-lookup"><span data-stu-id="f2165-124">These actions are unique tooeach application, and you should complete them along with hello steps provided in this guide toomake hello full transition tooPremium Storage as seamless as possible.</span></span>

## <span data-ttu-id="f2165-125"><a name="plan-the-migration-to-premium-storage"></a>Планирование миграции hello tooPremium хранилища</span><span class="sxs-lookup"><span data-stu-id="f2165-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for hello migration tooPremium Storage</span></span>
<span data-ttu-id="f2165-126">В этом разделе гарантирует, что будут готовы toofollow шагов миграции hello в этой статье и помогает toomake hello наилучшее решение в типах виртуальной Машины и диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-126">This section ensures that you are ready toofollow hello migration steps in this article, and helps you toomake hello best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f2165-127">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f2165-127">Prerequisites</span></span>
* <span data-ttu-id="f2165-128">Вам понадобится подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="f2165-128">You will need an Azure subscription.</span></span> <span data-ttu-id="f2165-129">Если у вас нет подписки, можно оформить [бесплатную пробную](https://azure.microsoft.com/pricing/free-trial/) подписку на один месяц или посетить страницу [Цены Azure](https://azure.microsoft.com/pricing/), чтобы ознакомиться с дополнительными возможностями.</span><span class="sxs-lookup"><span data-stu-id="f2165-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="f2165-130">tooexecute командлеты PowerShell, необходимо будет hello модуля Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2165-130">tooexecute PowerShell cmdlets, you will need hello Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="f2165-131">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для hello установить точку и инструкции по установке.</span><span class="sxs-lookup"><span data-stu-id="f2165-131">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello install point and installation instructions.</span></span>
* <span data-ttu-id="f2165-132">При планировании toouse Azure виртуальные машины на хранилище Premium необходимо hello toouse хранилище Premium поддерживает виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-132">When you plan toouse Azure VMs running on Premium Storage, you need toouse hello Premium Storage capable VMs.</span></span> <span data-ttu-id="f2165-133">С этими виртуальными машинами можно использовать диски хранилища класса Premium и Standard.</span><span class="sxs-lookup"><span data-stu-id="f2165-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="f2165-134">Диски хранилища Premium можно найти с несколько типов ВМ в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-134">Premium storage disks will be available with more VM types in hello future.</span></span> <span data-ttu-id="f2165-135">Дополнительные сведения о всех доступных типах и размерах дисков виртуальной машины Azure см. в разделах [Размеры виртуальных машин](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и [Размеры для облачных служб](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="f2165-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="f2165-136">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="f2165-136">Considerations</span></span>
<span data-ttu-id="f2165-137">Виртуальной машине Azure поддерживает подключение нескольких дисках хранилища Premium, чтобы приложения может содержать до too256 ТБ хранилища каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up too256 TB of storage per VM.</span></span> <span data-ttu-id="f2165-138">С хранилищем Premium вы получите выполнение до 80 000 операций ввода-вывода в секунду на виртуальную машину и пропускную способность второго диска до 2000 МБ в секунду на виртуальную машину с очень низкой задержкой при операциях чтения.</span><span class="sxs-lookup"><span data-stu-id="f2165-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="f2165-139">Вы можете выбирать виртуальные машины и диски среди множества различных вариантов.</span><span class="sxs-lookup"><span data-stu-id="f2165-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="f2165-140">Этот раздел представляет toohelp toofind параметр, который лучше всего подходит для рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f2165-140">This section is toohelp you toofind an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="f2165-141">Размеры виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="f2165-141">VM sizes</span></span>
<span data-ttu-id="f2165-142">Hello спецификаций размера виртуальной Машины Azure, перечислены в [размеры виртуальных машин](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2165-142">hello Azure VM size specifications are listed in [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f2165-143">Проверьте характеристики производительности hello виртуальные машины, работающие с хранилищем Premium и выберите размер виртуальной Машины наиболее подходящий hello, который лучше всего подходит для рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f2165-143">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="f2165-144">Убедитесь, что недоступна достаточную пропускную способность трафика диска виртуальной Машины toodrive hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-144">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="f2165-145">Размеры диска</span><span class="sxs-lookup"><span data-stu-id="f2165-145">Disk sizes</span></span>
<span data-ttu-id="f2165-146">Существуют пять типов дисков, которые можно использовать с виртуальной машиной. Для каждого из них действуют определенные ограничения на количество операций ввода-вывода в секунду и пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="f2165-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="f2165-147">При выборе типа hello диска для виртуальной Машины исходя из потребностей hello приложения с точки зрения производительности, производительность, масштабируемость и пиковых нагрузок учитывайте эти ограничения.</span><span class="sxs-lookup"><span data-stu-id="f2165-147">Take into consideration these limits when choosing hello disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="f2165-148">Диски уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="f2165-148">Premium Disks Type</span></span>  | <span data-ttu-id="f2165-149">P10</span><span class="sxs-lookup"><span data-stu-id="f2165-149">P10</span></span>   | <span data-ttu-id="f2165-150">P20</span><span class="sxs-lookup"><span data-stu-id="f2165-150">P20</span></span>   | <span data-ttu-id="f2165-151">P30</span><span class="sxs-lookup"><span data-stu-id="f2165-151">P30</span></span>            | <span data-ttu-id="f2165-152">P40</span><span class="sxs-lookup"><span data-stu-id="f2165-152">P40</span></span>            | <span data-ttu-id="f2165-153">P50</span><span class="sxs-lookup"><span data-stu-id="f2165-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="f2165-154">Размер диска</span><span class="sxs-lookup"><span data-stu-id="f2165-154">Disk size</span></span>           | <span data-ttu-id="f2165-155">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="f2165-155">128 GB</span></span>| <span data-ttu-id="f2165-156">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="f2165-156">512 GB</span></span>| <span data-ttu-id="f2165-157">1024 ГБ (1 ТБ)</span><span class="sxs-lookup"><span data-stu-id="f2165-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="f2165-158">2048 ГБ (2 ТБ)</span><span class="sxs-lookup"><span data-stu-id="f2165-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="f2165-159">4095 ГБ (4 ТБ)</span><span class="sxs-lookup"><span data-stu-id="f2165-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="f2165-160">Количество операций ввода-вывода в секунду на диск</span><span class="sxs-lookup"><span data-stu-id="f2165-160">IOPS per disk</span></span>       | <span data-ttu-id="f2165-161">500</span><span class="sxs-lookup"><span data-stu-id="f2165-161">500</span></span>   | <span data-ttu-id="f2165-162">2300</span><span class="sxs-lookup"><span data-stu-id="f2165-162">2300</span></span>  | <span data-ttu-id="f2165-163">5000</span><span class="sxs-lookup"><span data-stu-id="f2165-163">5000</span></span>           | <span data-ttu-id="f2165-164">7500</span><span class="sxs-lookup"><span data-stu-id="f2165-164">7500</span></span>           | <span data-ttu-id="f2165-165">7500</span><span class="sxs-lookup"><span data-stu-id="f2165-165">7500</span></span>           | 
| <span data-ttu-id="f2165-166">Пропускная способность на диск</span><span class="sxs-lookup"><span data-stu-id="f2165-166">Throughput per disk</span></span> | <span data-ttu-id="f2165-167">100 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="f2165-167">100 MB per second</span></span> | <span data-ttu-id="f2165-168">150 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="f2165-168">150 MB per second</span></span> | <span data-ttu-id="f2165-169">200 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="f2165-169">200 MB per second</span></span> | <span data-ttu-id="f2165-170">250 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="f2165-170">250 MB per second</span></span> | <span data-ttu-id="f2165-171">250 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="f2165-171">250 MB per second</span></span> |

<span data-ttu-id="f2165-172">В зависимости от рабочей нагрузки определите, требуются ли дополнительные диски данных для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="f2165-173">Можно присоединить несколько tooyour дисков постоянных данных виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-173">You can attach several persistent data disks tooyour VM.</span></span> <span data-ttu-id="f2165-174">При необходимости вы можете создать чередующийся через hello дисков tooincrease hello емкости и производительности hello тома.</span><span class="sxs-lookup"><span data-stu-id="f2165-174">If needed, you can stripe across hello disks tooincrease hello capacity and performance of hello volume.</span></span> <span data-ttu-id="f2165-175">(Дополнительные сведения о чередовании дисков см. [здесь](storage-premium-storage-performance.md#disk-striping).) Если вы создаете чередующийся том на дисках данных хранилища уровня "Премиум" с помощью [дисковых пространств][4], то необходимо настроить по одному столбцу для каждого используемого диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="f2165-176">В противном случае hello общую производительность hello чередующемся томе может быть ниже, чем ожидается, из-за toouneven распределение трафика между дисками hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-176">Otherwise, hello overall performance of hello striped volume may be lower than expected due toouneven distribution of traffic across hello disks.</span></span> <span data-ttu-id="f2165-177">Для виртуальных машин Linux можно использовать hello *mdadm* tooachieve программа hello таким же.</span><span class="sxs-lookup"><span data-stu-id="f2165-177">For Linux VMs you can use hello *mdadm* utility tooachieve hello same.</span></span> <span data-ttu-id="f2165-178">Дополнительные сведения см. в статье [Настройка программного RAID-массива в Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2165-178">See article [Configure Software RAID on Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="f2165-179">Целевые показатели масштабируемости для учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="f2165-179">Storage account scalability targets</span></span>
<span data-ttu-id="f2165-180">Учетные записи хранения Premium имеют следующие целевые показатели масштабируемости в toohello сложения hello [целевые показатели производительности и масштабируемости хранилища Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="f2165-180">Premium Storage accounts have hello following scalability targets in addition toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="f2165-181">Если требования вашего приложения превышают целевые показатели масштабируемости hello единым хранилища учетной записи, сборка toouse вашего приложения несколькими учетными записями хранения и секционировать данные по этим учетных записям хранения.</span><span class="sxs-lookup"><span data-stu-id="f2165-181">If your application requirements exceed hello scalability targets of a single storage account, build your application toouse multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="f2165-182">Общая емкость учетной записи</span><span class="sxs-lookup"><span data-stu-id="f2165-182">Total Account Capacity</span></span> | <span data-ttu-id="f2165-183">Общая пропускная способность для учетной записи локально избыточного хранилища</span><span class="sxs-lookup"><span data-stu-id="f2165-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2165-184">Емкость диска: 35 ТБ</span><span class="sxs-lookup"><span data-stu-id="f2165-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="f2165-185">Емкость для моментальных снимков: 10 ТБ</span><span class="sxs-lookup"><span data-stu-id="f2165-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="f2165-186">Копирование too50 гигабит в секунду входящие + исходящие</span><span class="sxs-lookup"><span data-stu-id="f2165-186">Up too50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="f2165-187">Для hello Дополнительные сведения о спецификациях хранилище Premium, ознакомьтесь с [масштабируемость и целевые показатели производительности при использовании хранилища Premium](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="f2165-187">For hello more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="f2165-188">Политика кэширования дисков</span><span class="sxs-lookup"><span data-stu-id="f2165-188">Disk caching policy</span></span>
<span data-ttu-id="f2165-189">По умолчанию политика кэширования диска — *только для чтения* для всех hello Premium дисков с данными и *чтения и записи* для диска операционной системы Premium hello присоединенного toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-189">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="f2165-190">Этот параметр конфигурации рекомендуется tooachieve hello оптимальную производительность операций ввода-вывода приложения.</span><span class="sxs-lookup"><span data-stu-id="f2165-190">This configuration setting is recommended tooachieve hello optimal performance for your application's IOs.</span></span> <span data-ttu-id="f2165-191">Отключите кэширование дисков данных, которые отличаются высокой интенсивностью записи или используются только для записи (например, файлов журналов SQL Server), чтобы улучшить производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="f2165-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="f2165-192">Параметры кэша Hello для существующих дисков данных можно обновить с помощью [портала Azure](https://portal.azure.com) или hello *- HostCaching* параметр hello *Set-AzureDataDisk* командлета.</span><span class="sxs-lookup"><span data-stu-id="f2165-192">hello cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or hello *-HostCaching* parameter of hello *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="f2165-193">Расположение</span><span class="sxs-lookup"><span data-stu-id="f2165-193">Location</span></span>
<span data-ttu-id="f2165-194">Выберите расположение, где доступно хранилище Azure Premium.</span><span class="sxs-lookup"><span data-stu-id="f2165-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="f2165-195">Актуальные сведения о доступных расположениях см. на странице [Доступность продуктов по регионам](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="f2165-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="f2165-196">Виртуальные машины находятся в hello же региона, как hello учетной записи хранилища, что магазины hello дисков для hello ВМ обеспечит гораздо более высокую производительность, чем если они находятся в отдельные области.</span><span class="sxs-lookup"><span data-stu-id="f2165-196">VMs located in hello same region as hello Storage account that stores hello disks for hello VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="f2165-197">Прочие параметры конфигурации виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="f2165-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="f2165-198">При создании виртуальной Машины Azure, будет задаваемые tooconfigure некоторые параметры виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-198">When creating an Azure VM, you will be asked tooconfigure certain VM settings.</span></span> <span data-ttu-id="f2165-199">Помните, что некоторые параметры имеют фиксированное время существования hello hello виртуальной Машины, хотя можно изменить или добавить другие позже.</span><span class="sxs-lookup"><span data-stu-id="f2165-199">Remember, few settings are fixed for hello lifetime of hello VM, while you can modify or add others later.</span></span> <span data-ttu-id="f2165-200">Просмотрите эти параметры конфигурации виртуальной Машины Azure и убедитесь в том, что они настроены правильно toomatch требований рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f2165-200">Review these Azure VM configuration settings and make sure that these are configured appropriately toomatch your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="f2165-201">Оптимизация</span><span class="sxs-lookup"><span data-stu-id="f2165-201">Optimization</span></span>
<span data-ttu-id="f2165-202">В статье [Хранилище Azure класса «Премиум»: разработка, обеспечивающая повышенную производительность](storage-premium-storage-performance.md) приведены рекомендации по разработке высокопроизводительных приложений с использованием хранилища Azure класса Premium.</span><span class="sxs-lookup"><span data-stu-id="f2165-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="f2165-203">Можно следовать правилам hello, в сочетании с производительности лучшие методики применимо tootechnologies, используемого приложением.</span><span class="sxs-lookup"><span data-stu-id="f2165-203">You can follow hello guidelines combined with performance best practices applicable tootechnologies used by your application.</span></span>

## <span data-ttu-id="f2165-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Подготовка и скопируйте виртуальные жесткие диски (VHD) tooPremium хранилища</span><span class="sxs-lookup"><span data-stu-id="f2165-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) tooPremium Storage</span></span>
<span data-ttu-id="f2165-205">Hello в следующем разделе содержатся рекомендации по подготовке виртуальных жестких дисков из виртуальной Машины и копирование виртуальных жестких дисков tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="f2165-205">hello following section provides guidelines for preparing VHDs from your VM and copying VHDs tooAzure Storage.</span></span>

* [<span data-ttu-id="f2165-206">Сценарий 1: «я перехожу существующих виртуальных машинах Azure tooAzure хранилище Premium.»</span><span class="sxs-lookup"><span data-stu-id="f2165-206">Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="f2165-207">Сценарий 2: «я перехожу виртуальные машины из других платформ tooAzure хранилище Premium.»</span><span class="sxs-lookup"><span data-stu-id="f2165-207">Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="f2165-208">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f2165-208">Prerequisites</span></span>
<span data-ttu-id="f2165-209">hello tooprepare виртуальные жесткие диски для миграции, необходимо:</span><span class="sxs-lookup"><span data-stu-id="f2165-209">tooprepare hello VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="f2165-210">Подписка Azure, учетной записи хранилища и контейнера в этом хранилище учетной записи toowhich, можно скопировать вашего виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-210">An Azure subscription, a storage account, and a container in that storage account toowhich you can copy your VHD.</span></span> <span data-ttu-id="f2165-211">Обратите внимание, что hello целевой учетной записью хранения может быть учетной записью Standard или Premium хранилища, в зависимости от ваших требований.</span><span class="sxs-lookup"><span data-stu-id="f2165-211">Note that hello destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="f2165-212">Hello toogeneralize средство виртуального жесткого диска, если планируется toocreate несколько экземпляров виртуальных Машин из него.</span><span class="sxs-lookup"><span data-stu-id="f2165-212">A tool toogeneralize hello VHD if you plan toocreate multiple VM instances from it.</span></span> <span data-ttu-id="f2165-213">Например, sysprep для Windows или virt-sysprep для Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f2165-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="f2165-214">Средство tooupload hello VHD файл toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="f2165-214">A tool tooupload hello VHD file toohello Storage account.</span></span> <span data-ttu-id="f2165-215">В разделе [перенесите данные с помощью служебной программы командной строки AzCopy hello](storage-use-azcopy.md) или использовать [обозреватель хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2165-215">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="f2165-216">В этом руководстве описано копирование вашего виртуального жесткого диска, с помощью инструмента AzCopy hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-216">This guide describes copying your VHD using hello AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="f2165-217">При выборе параметра синхронного копирования с помощью AzCopy, для обеспечения оптимальной производительности, скопируйте вашего виртуального жесткого диска, выполнив одно из этих средств из виртуальной Машины Azure, hello же регионе, что hello целевой учетной записью хранения.</span><span class="sxs-lookup"><span data-stu-id="f2165-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in hello same region as hello destination storage account.</span></span> <span data-ttu-id="f2165-218">При копировании виртуального жесткого диска из виртуальной машины Azure в другом регионе производительность может быть ниже.</span><span class="sxs-lookup"><span data-stu-id="f2165-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="f2165-219">При копировании ограниченной пропускной способностью большой объем данных, рассмотрите возможность [tooBlob hello импорта и экспорта Azure службы tootransfer данные хранилища с помощью](storage-import-export-service.md); это позволяет tootransfer tooan Azure диски данных путем доставки жесткого диска Центр обработки данных.</span><span class="sxs-lookup"><span data-stu-id="f2165-219">For copying a large amount of data over limited bandwidth, consider [using hello Azure Import/Export service tootransfer data tooBlob Storage](storage-import-export-service.md); this allows you tootransfer your data by shipping hard disk drives tooan Azure datacenter.</span></span> <span data-ttu-id="f2165-220">Можно использовать hello импорта и экспорта Azure toocopy данных tooa стандартное хранилище учетной записи службы только.</span><span class="sxs-lookup"><span data-stu-id="f2165-220">You can use hello Azure Import/Export service toocopy data tooa standard storage account only.</span></span> <span data-ttu-id="f2165-221">После hello данные хранятся в учетной записи хранения standard, можно использовать либо hello [API копирования BLOB-объектов](https://msdn.microsoft.com/library/azure/dd894037.aspx) или AzCopy tootransfer hello данных tooyour premium учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="f2165-221">Once hello data is in your standard storage account, you can use either hello [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy tootransfer hello data tooyour premium storage account.</span></span>
>
> <span data-ttu-id="f2165-222">Обратите внимание, что Microsoft Azure поддерживает только файлы виртуальных жестких дисков фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="f2165-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="f2165-223">VHDX-файлы или динамические виртуальные жесткие диски не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="f2165-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="f2165-224">При наличии динамического виртуального жесткого диска, можно преобразовать его с помощью hello размер toofixed [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="f2165-224">If you have a dynamic VHD, you can convert it toofixed size using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="f2165-225"><a name="scenario1"></a>Сценарий 1: «я перехожу существующих виртуальных машинах Azure tooAzure хранилище Premium.»</span><span class="sxs-lookup"><span data-stu-id="f2165-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>
<span data-ttu-id="f2165-226">При переносе существующих виртуальных машинах Azure, hello остановка виртуальной Машины, виртуальные жесткие диски каждого типа hello виртуального жесткого диска, необходимо подготовить и скопируйте hello виртуального жесткого диска с помощью AzCopy или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2165-226">If you are migrating existing Azure VMs, stop hello VM, prepare VHDs per hello type of VHD you want, and then copy hello VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="f2165-227">Hello виртуальной Машины должен toobe полностью вниз toomigrate исходное состояние.</span><span class="sxs-lookup"><span data-stu-id="f2165-227">hello VM needs toobe completely down toomigrate a clean state.</span></span> <span data-ttu-id="f2165-228">До завершения миграции hello будет простоя.</span><span class="sxs-lookup"><span data-stu-id="f2165-228">There will be a downtime until hello migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="f2165-229">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="f2165-229">Step 1.</span></span> <span data-ttu-id="f2165-230">Подготовка VHD к переносу</span><span class="sxs-lookup"><span data-stu-id="f2165-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="f2165-231">При переносе существующих виртуальных машинах Azure tooPremium хранилища, то виртуальный ДИСК может быть:</span><span class="sxs-lookup"><span data-stu-id="f2165-231">If you are migrating existing Azure VMs tooPremium Storage, your VHD may be:</span></span>

* <span data-ttu-id="f2165-232">обобщенный образ операционной системы;</span><span class="sxs-lookup"><span data-stu-id="f2165-232">A generalized operating system image</span></span>
* <span data-ttu-id="f2165-233">уникальный диск операционной системы;</span><span class="sxs-lookup"><span data-stu-id="f2165-233">A unique operating system disk</span></span>
* <span data-ttu-id="f2165-234">диск данных.</span><span class="sxs-lookup"><span data-stu-id="f2165-234">A data disk</span></span>

<span data-ttu-id="f2165-235">Ниже рассмотрены три соответствующих сценария подготовки VHD.</span><span class="sxs-lookup"><span data-stu-id="f2165-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a><span data-ttu-id="f2165-236">Использовать несколько экземпляров ВМ обобщенный toocreate виртуального жесткого диска операционной системы</span><span class="sxs-lookup"><span data-stu-id="f2165-236">Use a generalized Operating System VHD toocreate multiple VM instances</span></span>
<span data-ttu-id="f2165-237">При выгрузке виртуального жесткого диска, который будет использоваться toocreate несколько экземпляров универсального виртуальной Машине Azure, сначала необходимо обобщить виртуального жесткого диска с помощью программы sysprep.</span><span class="sxs-lookup"><span data-stu-id="f2165-237">If you are uploading a VHD that will be used toocreate multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="f2165-238">Это относится tooa виртуального жесткого диска, локально или в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-238">This applies tooa VHD that is on-premises or in hello cloud.</span></span> <span data-ttu-id="f2165-239">Удаляются все сведения, относящиеся к машине из hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-239">Sysprep removes any machine-specific information from hello VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2165-240">Создайте моментальный снимок или резервную копию виртуальной машины перед ее обобщением.</span><span class="sxs-lookup"><span data-stu-id="f2165-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="f2165-241">Выполнение средства sysprep будет останавливать и освобождать hello экземпляр виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-241">Running sysprep will stop and deallocate hello VM instance.</span></span> <span data-ttu-id="f2165-242">Выполните действия ниже toosysprep виртуального жесткого диска операционной системы Windows.</span><span class="sxs-lookup"><span data-stu-id="f2165-242">Follow steps below toosysprep a Windows OS VHD.</span></span> <span data-ttu-id="f2165-243">Обратите внимание, что выполнив команду Sysprep hello потребует tooshut работу виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-243">Note that running hello Sysprep command will require you tooshut down hello virtual machine.</span></span> <span data-ttu-id="f2165-244">Дополнительные сведения о команде Sysprep см. в разделах [Обзор Sysprep](http://technet.microsoft.com/library/hh825209.aspx) или [Технический справочник по Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2165-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="f2165-245">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="f2165-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="f2165-246">Введите следующая команда tooopen Sysprep hello:</span><span class="sxs-lookup"><span data-stu-id="f2165-246">Enter hello following command tooopen Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="f2165-247">В hello средство подготовки системы, выберите выберите Enter System Out-of-Box Experience (OOBE), выберите hello Generalize флажок **завершение работы**, а затем нажмите кнопку **ОК**, как показано в приведенном ниже рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-247">In hello System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select hello Generalize check box, select **Shutdown**, and then click **OK**, as shown in hello image below.</span></span> <span data-ttu-id="f2165-248">Sysprep будет generalize hello операционной системы и завершение работы системы hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-248">Sysprep will generalize hello operating system and shut down hello system.</span></span>

    ![][1]

<span data-ttu-id="f2165-249">Для Виртуальной машине Ubuntu используйте virt sysprep tooachieve hello таким же.</span><span class="sxs-lookup"><span data-stu-id="f2165-249">For an Ubuntu VM, use virt-sysprep tooachieve hello same.</span></span> <span data-ttu-id="f2165-250">Дополнительные сведения см. в разделе [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html).</span><span class="sxs-lookup"><span data-stu-id="f2165-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="f2165-251">См. также некоторые Привет открыть источник [Подготовка сервера Linux программного обеспечения](http://www.cyberciti.biz/tips/server-provisioning-software.html) для других операционных систем Linux.</span><span class="sxs-lookup"><span data-stu-id="f2165-251">See also some of hello open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a><span data-ttu-id="f2165-252">Используйте уникальный toocreate виртуального жесткого диска операционной системы один экземпляр виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="f2165-252">Use a unique Operating System VHD toocreate a single VM instance</span></span>
<span data-ttu-id="f2165-253">При наличии приложения, работающего на ВМ, для которой требуются определенные данные машина hello hello не подходит hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-253">If you have an application running on hello VM which requires hello machine specific data, do not generalize hello VHD.</span></span> <span data-ttu-id="f2165-254">Специализированного виртуального жесткого диска можно использовать toocreate уникальный экземпляр виртуальной Машины Azure.</span><span class="sxs-lookup"><span data-stu-id="f2165-254">A non-generalized VHD can be used toocreate a unique Azure VM instance.</span></span> <span data-ttu-id="f2165-255">Например, при наличии контроллера домена на вашем виртуальном жестком диске выполнение команды sysprep сделает его неэффективным в качестве контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="f2165-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="f2165-256">Просмотрите hello приложений, выполняющихся на вашей виртуальной Машины и hello влияние запуск sysprep в их перед обобщение hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-256">Review hello applications running on your VM and hello impact of running sysprep on them before generalizing hello VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="f2165-257">Регистрация VHD в качестве диска данных</span><span class="sxs-lookup"><span data-stu-id="f2165-257">Register data disk VHD</span></span>
<span data-ttu-id="f2165-258">Если диски с данными в Azure toobe миграции, необходимо убедиться, что hello виртуальных машин, использующих эти диски, завершают работу данных.</span><span class="sxs-lookup"><span data-stu-id="f2165-258">If you have data disks in Azure toobe migrated, you must make sure hello VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="f2165-259">Выполните описанные ниже tooAzure VHD toocopy хранилище Premium действия hello и зарегистрировать его в качестве диска подготовленных данных.</span><span class="sxs-lookup"><span data-stu-id="f2165-259">Follow hello steps described below toocopy VHD tooAzure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="f2165-260">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="f2165-260">Step 2.</span></span> <span data-ttu-id="f2165-261">Создание назначения hello для вашего виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="f2165-261">Create hello destination for your VHD</span></span>
<span data-ttu-id="f2165-262">Создайте учетную запись хранения для обслуживания виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="f2165-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="f2165-263">Рассмотрим следующие точки при планировании расположения hello toostore виртуальные жесткие диски:</span><span class="sxs-lookup"><span data-stu-id="f2165-263">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="f2165-264">Hello целевой учетной записи хранения Premium.</span><span class="sxs-lookup"><span data-stu-id="f2165-264">hello target Premium storage account.</span></span>
* <span data-ttu-id="f2165-265">расположение учетной записи хранения Hello должен быть такой же, как хранилище Premium поддерживает виртуальные машины Azure создаст заключительном этапе hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-265">hello storage account location must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="f2165-266">Можно скопировать tooa новой учетной записи хранения или учетную запись хранения зависимости от потребностей hello toouse плана.</span><span class="sxs-lookup"><span data-stu-id="f2165-266">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="f2165-267">Скопируйте и сохраните ключ учетной записи хранения hello учетной записи хранения hello назначения для следующего этапа hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-267">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="f2165-268">Для дисков данных вы можете tookeep некоторые диски с данными в стандартном хранилище учетной записи (например, диски, имеющие охлаждающего хранилище), но настоятельно рекомендуется переместить все данные хранилища уровня premium toouse рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f2165-268">For data disks, you can choose tookeep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <span data-ttu-id="f2165-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="f2165-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="f2165-270">Копирование VHD с помощью AzCopy или PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2165-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="f2165-271">Необходимо будет toofind путь контейнера и хранения данных учетной записи ключа tooprocess любой из этих двух параметров.</span><span class="sxs-lookup"><span data-stu-id="f2165-271">You will need toofind your container path and storage account key tooprocess either of these two options.</span></span> <span data-ttu-id="f2165-272">(выберите **Портал Azure** > **Хранилище**, чтобы узнать их).</span><span class="sxs-lookup"><span data-stu-id="f2165-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="f2165-273">URL-адрес контейнера Hello будет отображаться как «https://myaccount.blob.core.windows.net/mycontainer/».</span><span class="sxs-lookup"><span data-stu-id="f2165-273">hello container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="f2165-274">Способ 1. Копирование VHD с помощью AzCopy (асинхронное копирование)</span><span class="sxs-lookup"><span data-stu-id="f2165-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="f2165-275">С помощью AzCopy, который можно передать hello виртуальный жесткий ДИСК через Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-275">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="f2165-276">В зависимости от размера hello hello виртуальные жесткие диски это может занять время.</span><span class="sxs-lookup"><span data-stu-id="f2165-276">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="f2165-277">При использовании этого параметра следует помните ограничения Исходящие и входящие данные учетной записи хранения toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-277">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="f2165-278">Дополнительные сведения см. в статье [Целевые показатели производительности и масштабируемости службы хранилища Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="f2165-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="f2165-279">Загрузите и установите AzCopy по ссылке: [последняя версия AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="f2165-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="f2165-280">Откройте Azure PowerShell и перейдите toohello папка, содержащая AzCopy.</span><span class="sxs-lookup"><span data-stu-id="f2165-280">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="f2165-281">Используйте hello следующая команда toocopy hello VHD-файл из «Источник» слишком «Назначение».</span><span class="sxs-lookup"><span data-stu-id="f2165-281">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="f2165-282">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2165-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="f2165-283">Ниже приведены описания параметров hello, используемых в hello команды AzCopy.</span><span class="sxs-lookup"><span data-stu-id="f2165-283">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="f2165-284">**-Источник:  *&lt;источника&gt;:***  hello папки или URL-адрес хранилища контейнер, содержащий hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-284">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="f2165-285">**/ SourceKey:  *&lt;ключ учетной записи источника&gt;:***  ключ учетной записи хранилища учетной записи хранения источника hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="f2165-286">**/ Dest:  *&lt;назначения&gt;:***  toocopy URL-адрес контейнера хранилища hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-286">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="f2165-287">**/ DestKey:  *&lt;ключ для учетной записи dest&gt;:***  ключ учетной записи хранилища учетной записи хранения назначения hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="f2165-288">**Или: шаблон  *&lt;имя файла&gt;:***  укажите имя файла hello toocopy hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-288">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="f2165-289">Дополнительные сведения об использовании AzCopy инструментов см. в разделе [перенесите данные с помощью служебной программы командной строки AzCopy hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="f2165-289">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="f2165-290">Способ 2. Копирование VHD с помощью PowerShell (синхронное копирование)</span><span class="sxs-lookup"><span data-stu-id="f2165-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="f2165-291">Также можно скопировать hello VHD-файл с помощью командлета PowerShell hello AzureStorageBlobCopy запуска.</span><span class="sxs-lookup"><span data-stu-id="f2165-291">You can also copy hello VHD file using hello PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="f2165-292">Используйте следующую команду на Azure PowerShell toocopy VHD hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-292">Use hello following command on Azure PowerShell toocopy VHD.</span></span> <span data-ttu-id="f2165-293">Замените значения hello в угловых скобках соответствующими значениями из источника и назначения учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="f2165-293">Replace hello values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="f2165-294">toouse эту команду, необходимо иметь контейнер с именем виртуальные жесткие диски в целевой учетной записью хранения.</span><span class="sxs-lookup"><span data-stu-id="f2165-294">toouse this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="f2165-295">Если контейнер hello не существует, создайте его перед выполнением команды hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-295">If hello container doesn't exist, create one before running hello command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="f2165-296">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2165-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="f2165-297"><a name="scenario2"></a>Сценарий 2: «я перехожу виртуальные машины из других платформ tooAzure хранилище Premium.»</span><span class="sxs-lookup"><span data-stu-id="f2165-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>
<span data-ttu-id="f2165-298">При переносе виртуального жесткого диска из tooAzure не Azure облачного хранилища, необходимо экспортировать hello VHD tooa локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="f2165-298">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="f2165-299">Полный исходный путь hello hello локальный каталог, где хранится под рукой виртуального жесткого диска, а затем с помощью AzCopy tooupload его tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="f2165-299">Have hello complete source path of hello local directory where VHD is stored handy, and then using AzCopy tooupload it tooAzure Storage.</span></span>

#### <a name="step-1-export-vhd-tooa-local-directory"></a><span data-ttu-id="f2165-300">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="f2165-300">Step 1.</span></span> <span data-ttu-id="f2165-301">Экспорт локальный каталог tooa виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="f2165-301">Export VHD tooa local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="f2165-302">Копирование VHD из AWS</span><span class="sxs-lookup"><span data-stu-id="f2165-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="f2165-303">Если вы используете AWS, экспортируйте hello EC2 экземпляр tooa виртуального жесткого диска в сегмент Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="f2165-303">If you are using AWS, export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="f2165-304">Следуйте hello действия, описанные в документации Amazon для экспорта экземпляров EC2 Amazon tooinstall hello Amazon EC2 командной строки (CLI) средства hello и запустите hello команда создания экземпляра export задач tooexport hello EC2 экземпляр tooa VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="f2165-304">Follow hello steps described in hello Amazon documentation for Exporting Amazon EC2 Instances tooinstall hello Amazon EC2 command-line interface (CLI) tool and run hello create-instance-export-task command tooexport hello EC2 instance tooa VHD file.</span></span> <span data-ttu-id="f2165-305">Быть убедиться, что toouse **VHD** для hello диска &#95; образ &#95; ФОРМАТ переменной при выполнении hello **создания экземпляра export задач** команды.</span><span class="sxs-lookup"><span data-stu-id="f2165-305">Be sure toouse **VHD** for hello DISK&#95;IMAGE&#95;FORMAT variable when running hello **create-instance-export-task** command.</span></span> <span data-ttu-id="f2165-306">Hello экспортированный файл VHD сохраняется в контейнере hello Amazon S3, определенное во время этого процесса.</span><span class="sxs-lookup"><span data-stu-id="f2165-306">hello exported VHD file is saved in hello Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="f2165-307">Загрузите файл виртуального жесткого диска hello с сегмент S3 hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-307">Download hello VHD file from hello S3 bucket.</span></span> <span data-ttu-id="f2165-308">Выберите hello VHD-файл, затем **действия** > **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="f2165-308">Select hello VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="f2165-309">Копирование VHD из облака (вне Azure)</span><span class="sxs-lookup"><span data-stu-id="f2165-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="f2165-310">При переносе виртуального жесткого диска из tooAzure не Azure облачного хранилища, необходимо экспортировать hello VHD tooa локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="f2165-310">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="f2165-311">Скопируйте полный исходный путь hello hello локальный каталог, где хранится виртуальный жесткий ДИСК.</span><span class="sxs-lookup"><span data-stu-id="f2165-311">Copy hello complete source path of hello local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="f2165-312">Копирование VHD из локальной среды</span><span class="sxs-lookup"><span data-stu-id="f2165-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="f2165-313">Если вы переносите VHD из локальной среды, необходимо будет hello полный исходный путь, где хранится виртуальный жесткий ДИСК.</span><span class="sxs-lookup"><span data-stu-id="f2165-313">If you are migrating VHD from an on-premises environment, you will need hello complete source path where VHD is stored.</span></span> <span data-ttu-id="f2165-314">Hello исходный путь может быть server расположение или в общей папке.</span><span class="sxs-lookup"><span data-stu-id="f2165-314">hello source path could be a server location or file share.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="f2165-315">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="f2165-315">Step 2.</span></span> <span data-ttu-id="f2165-316">Создание назначения hello для вашего виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="f2165-316">Create hello destination for your VHD</span></span>
<span data-ttu-id="f2165-317">Создайте учетную запись хранения для обслуживания виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="f2165-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="f2165-318">Рассмотрим следующие точки при планировании расположения hello toostore виртуальные жесткие диски:</span><span class="sxs-lookup"><span data-stu-id="f2165-318">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="f2165-319">Hello целевой учетной записи хранения может быть стандартного или расширенного хранилища в зависимости от требований приложения.</span><span class="sxs-lookup"><span data-stu-id="f2165-319">hello target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="f2165-320">Хранилище Premium поддерживает виртуальные машины Azure создаст заключительном этапе hello должен совпадать Hello регион учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="f2165-320">hello storage account region must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="f2165-321">Можно скопировать tooa новой учетной записи хранения или учетную запись хранения зависимости от потребностей hello toouse плана.</span><span class="sxs-lookup"><span data-stu-id="f2165-321">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="f2165-322">Скопируйте и сохраните ключ учетной записи хранения hello учетной записи хранения hello назначения для следующего этапа hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-322">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="f2165-323">Мы настоятельно рекомендуем вам перемещение всех данных для хранения premium toouse рабочей рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f2165-323">We strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a><span data-ttu-id="f2165-324">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="f2165-324">Step 3.</span></span> <span data-ttu-id="f2165-325">Отправка VHD hello tooAzure хранилища</span><span class="sxs-lookup"><span data-stu-id="f2165-325">Upload hello VHD tooAzure Storage</span></span>
<span data-ttu-id="f2165-326">Теперь, когда имеется вашего виртуального жесткого диска в локальном каталоге hello, можно использовать AzCopy или AzurePowerShell tooupload hello .vhd файл tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="f2165-326">Now that you have your VHD in hello local directory, you can use AzCopy or AzurePowerShell tooupload hello .vhd file tooAzure Storage.</span></span> <span data-ttu-id="f2165-327">Это можно сделать двумя способами.</span><span class="sxs-lookup"><span data-stu-id="f2165-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a><span data-ttu-id="f2165-328">Вариант 1: С помощью Azure PowerShell Add-AzureVhd tooupload hello VHD-файл</span><span class="sxs-lookup"><span data-stu-id="f2165-328">Option 1: Using Azure PowerShell Add-AzureVhd tooupload hello .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="f2165-329">Пример <Uri> может выглядеть следующим образом: ***https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd***.</span><span class="sxs-lookup"><span data-stu-id="f2165-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="f2165-330">Пример <FileInfo>: ***C:\path\to\upload.vhd***.</span><span class="sxs-lookup"><span data-stu-id="f2165-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a><span data-ttu-id="f2165-331">Вариант 2: С помощью AzCopy tooupload hello VHD-файл</span><span class="sxs-lookup"><span data-stu-id="f2165-331">Option 2: Using AzCopy tooupload hello .vhd file</span></span>
<span data-ttu-id="f2165-332">С помощью AzCopy, который можно передать hello виртуальный жесткий ДИСК через Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-332">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="f2165-333">В зависимости от размера hello hello виртуальные жесткие диски это может занять время.</span><span class="sxs-lookup"><span data-stu-id="f2165-333">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="f2165-334">При использовании этого параметра следует помните ограничения Исходящие и входящие данные учетной записи хранения toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-334">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="f2165-335">Дополнительные сведения см. в статье [Целевые показатели производительности и масштабируемости службы хранилища Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="f2165-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="f2165-336">Загрузите и установите AzCopy по ссылке: [последняя версия AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="f2165-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="f2165-337">Откройте Azure PowerShell и перейдите toohello папка, содержащая AzCopy.</span><span class="sxs-lookup"><span data-stu-id="f2165-337">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="f2165-338">Используйте hello следующая команда toocopy hello VHD-файл из «Источник» слишком «Назначение».</span><span class="sxs-lookup"><span data-stu-id="f2165-338">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="f2165-339">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2165-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="f2165-340">Ниже приведены описания параметров hello, используемых в hello команды AzCopy.</span><span class="sxs-lookup"><span data-stu-id="f2165-340">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="f2165-341">**-Источник:  *&lt;источника&gt;:***  hello папки или URL-адрес хранилища контейнер, содержащий hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-341">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="f2165-342">**/ SourceKey:  *&lt;ключ учетной записи источника&gt;:***  ключ учетной записи хранилища учетной записи хранения источника hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="f2165-343">**/ Dest:  *&lt;назначения&gt;:***  toocopy URL-адрес контейнера хранилища hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-343">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="f2165-344">**/ DestKey:  *&lt;ключ для учетной записи dest&gt;:***  ключ учетной записи хранилища учетной записи хранения назначения hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="f2165-345">**/ BlobType: страница:** указывает указанное назначение hello страничного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="f2165-345">**/BlobType: page:** Specifies that hello destination is a page blob.</span></span>
   * <span data-ttu-id="f2165-346">**Или: шаблон  *&lt;имя файла&gt;:***  укажите имя файла hello toocopy hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-346">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="f2165-347">Дополнительные сведения об использовании AzCopy инструментов см. в разделе [перенесите данные с помощью служебной программы командной строки AzCopy hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="f2165-347">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="f2165-348">Другие возможности загрузки виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="f2165-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="f2165-349">Можно также передать учетную запись хранения tooyour виртуального жесткого диска с помощью одного из hello следующие средства:</span><span class="sxs-lookup"><span data-stu-id="f2165-349">You can also upload a VHD tooyour storage account using one of hello following means:</span></span>

* [<span data-ttu-id="f2165-350">API копирования BLOB-объекта хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="f2165-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="f2165-351">Обозреватель хранилищ Azure для передачи больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="f2165-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="f2165-352">Справочник по API REST служб хранилища импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="f2165-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="f2165-353">Мы рекомендуем использовать службу импорта и экспорта, если предполагаемое время передачи больше 7 дней.</span><span class="sxs-lookup"><span data-stu-id="f2165-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="f2165-354">Можно использовать [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate время hello из единицу размера и передачи данных.</span><span class="sxs-lookup"><span data-stu-id="f2165-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="f2165-355">Импорт и экспорт можно использовать toocopy tooa Стандартная учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="f2165-355">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="f2165-356">Вам потребуется toocopy из учетной записи хранения toopremium стандартного хранилища с помощью таких средств, как AzCopy.</span><span class="sxs-lookup"><span data-stu-id="f2165-356">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="f2165-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Создание виртуальной машины Azure с использованием хранилища Premium</span><span class="sxs-lookup"><span data-stu-id="f2165-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="f2165-358">После учетной записи хранения загруженного или скопированного toohello требуемого hello виртуального жесткого диска следуйте инструкциям hello в этот раздел tooregister hello VHD как образ ОС или диска ОС, в зависимости от вашего сценария, а затем создайте экземпляр виртуальной Машины из него.</span><span class="sxs-lookup"><span data-stu-id="f2165-358">After hello VHD is uploaded or copied toohello desired storage account, follow hello instructions in this section tooregister hello VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="f2165-359">Hello диск данных виртуального жесткого диска может быть вложенного toohello виртуальной Машины, после его создания.</span><span class="sxs-lookup"><span data-stu-id="f2165-359">hello data disk VHD can be attached toohello VM once it is created.</span></span>
<span data-ttu-id="f2165-360">В конце hello в этом разделе предоставляется пример сценария миграции.</span><span class="sxs-lookup"><span data-stu-id="f2165-360">A sample migration script is provided at hello end of this section.</span></span> <span data-ttu-id="f2165-361">Это простой скрипт, и он подходит не для всех сценариев.</span><span class="sxs-lookup"><span data-stu-id="f2165-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="f2165-362">Может потребоваться сценарий toomatch tooupdate hello с конкретного сценария.</span><span class="sxs-lookup"><span data-stu-id="f2165-362">You may need tooupdate hello script toomatch with your specific scenario.</span></span> <span data-ttu-id="f2165-363">см. ниже toosee, если этот сценарий применяется сценарий tooyour [сценарий миграции](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="f2165-363">toosee if this script applies tooyour scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="f2165-364">Контрольный список</span><span class="sxs-lookup"><span data-stu-id="f2165-364">Checklist</span></span>
1. <span data-ttu-id="f2165-365">Подождать, пока все диски VHD hello копирования завершена.</span><span class="sxs-lookup"><span data-stu-id="f2165-365">Wait until all hello VHD disks copying is complete.</span></span>
2. <span data-ttu-id="f2165-366">Убедитесь, что хранилище Premium доступно в области hello, которую вы переносите.</span><span class="sxs-lookup"><span data-stu-id="f2165-366">Make sure Premium Storage is available in hello region you are migrating to.</span></span>
3. <span data-ttu-id="f2165-367">Решите, Серия виртуальных Машин новый hello, который будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="f2165-367">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="f2165-368">Должно быть хранения Premium может и hello размер должен быть в зависимости от доступности hello в регионе hello и зависимости от потребностей.</span><span class="sxs-lookup"><span data-stu-id="f2165-368">It should be a Premium Storage capable, and hello size should be depending on hello availability in hello region and based on your needs.</span></span>
4. <span data-ttu-id="f2165-369">Выберите размер виртуальной Машины точное hello, который будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="f2165-369">Decide hello exact VM size you will use.</span></span> <span data-ttu-id="f2165-370">Размер виртуальной Машины должен toobe достаточно большой toosupport hello количество дисков данных вами.</span><span class="sxs-lookup"><span data-stu-id="f2165-370">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="f2165-371">Например: </span><span class="sxs-lookup"><span data-stu-id="f2165-371">E.g.</span></span> <span data-ttu-id="f2165-372">При наличии 4 диска данных hello ВМ необходимо иметь 2 или более ядер.</span><span class="sxs-lookup"><span data-stu-id="f2165-372">if you have 4 data disks, hello VM must have 2 or more cores.</span></span> <span data-ttu-id="f2165-373">Кроме того, учитывайте требования к вычислительной мощности, памяти и пропускной способности сети.</span><span class="sxs-lookup"><span data-stu-id="f2165-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="f2165-374">Создайте учетную запись хранения Premium в целевой области hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-374">Create a Premium Storage account in hello target region.</span></span> <span data-ttu-id="f2165-375">Это hello учетная запись будет использоваться для hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-375">This is hello account you will use for hello new VM.</span></span>
6. <span data-ttu-id="f2165-376">Иметь hello текущей виртуальной Машины сведений под рукой, включая hello список дисков и соответствующих больших двоичных объектов VHD.</span><span class="sxs-lookup"><span data-stu-id="f2165-376">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="f2165-377">Подготовьте приложение к простою.</span><span class="sxs-lookup"><span data-stu-id="f2165-377">Prepare your application for downtime.</span></span> <span data-ttu-id="f2165-378">toodo очистить миграции у вас toostop вся обработка hello в текущей системе hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-378">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="f2165-379">Только после этого можно получить его состояние tooconsistent, который можно перенести toohello новой платформы.</span><span class="sxs-lookup"><span data-stu-id="f2165-379">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="f2165-380">Длительность времени простоя будет зависеть от hello объем данных в toomigrate диски hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-380">Downtime duration will depend on hello amount of data in hello disks toomigrate.</span></span>

> [!NOTE]
> <span data-ttu-id="f2165-381">При создании виртуальной Машины диспетчера ресурсов Azure из специализированного диска VHD можно найти слишком[этот шаблон](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) для развертывания виртуальных Машин диспетчера ресурсов с помощью существующего диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer too[this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="f2165-382">Регистрация виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="f2165-382">Register your VHD</span></span>
<span data-ttu-id="f2165-383">toocreate виртуальной Машины из виртуального жесткого диска операционной системы или диска данных tooa tooattach новой виртуальной Машины, необходимо сначала зарегистрировать их.</span><span class="sxs-lookup"><span data-stu-id="f2165-383">toocreate a VM from OS VHD or tooattach a data disk tooa new VM, you must first register them.</span></span> <span data-ttu-id="f2165-384">Выполните приведенные ниже шаги в зависимости от сценария VHD.</span><span class="sxs-lookup"><span data-stu-id="f2165-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="f2165-385">Обобщенный виртуальный жесткий ДИСК операционной системы toocreate несколько экземпляров виртуальной Машины Azure</span><span class="sxs-lookup"><span data-stu-id="f2165-385">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="f2165-386">После передачи обобщенный образ ОС, виртуального жесткого диска является учетная запись хранения toohello зарегистрировать ее в качестве **образа виртуальной Машины Azure** , чтобы один или несколько экземпляров виртуальной Машины можно создать из него.</span><span class="sxs-lookup"><span data-stu-id="f2165-386">After generalized OS image VHD is uploaded toohello storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="f2165-387">Используйте следующие tooregister командлеты PowerShell hello вашего виртуального жесткого диска как образ ОС виртуальной Машины Azure.</span><span class="sxs-lookup"><span data-stu-id="f2165-387">Use hello following PowerShell cmdlets tooregister your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="f2165-388">Укажите полный контейнера hello URL-адрес, где виртуальный жесткий ДИСК был скопирован.</span><span class="sxs-lookup"><span data-stu-id="f2165-388">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="f2165-389">Скопируйте и сохраните имя hello этот новый образ виртуальной Машины Azure.</span><span class="sxs-lookup"><span data-stu-id="f2165-389">Copy and save hello name of this new Azure VM Image.</span></span> <span data-ttu-id="f2165-390">В приведенном выше примере hello, это *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="f2165-390">In hello example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="f2165-391">Уникальный виртуального жесткого диска операционной системы toocreate один экземпляр виртуальной Машины Azure</span><span class="sxs-lookup"><span data-stu-id="f2165-391">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="f2165-392">После hello уникальный виртуального жесткого диска ОС — хранилище отправленного toohello учетной записи, зарегистрируйте его как **диска ОС Azure** , чтобы экземпляр виртуальной Машины можно создать из него.</span><span class="sxs-lookup"><span data-stu-id="f2165-392">After hello unique OS VHD is uploaded toohello storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="f2165-393">Используйте эти tooregister командлеты PowerShell вашего виртуального жесткого диска в качестве диска ОС Azure.</span><span class="sxs-lookup"><span data-stu-id="f2165-393">Use these PowerShell cmdlets tooregister your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="f2165-394">Укажите полный контейнера hello URL-адрес, где виртуальный жесткий ДИСК был скопирован.</span><span class="sxs-lookup"><span data-stu-id="f2165-394">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="f2165-395">Скопируйте и сохраните имя hello этот новый диск ОС Azure.</span><span class="sxs-lookup"><span data-stu-id="f2165-395">Copy and save hello name of this new Azure OS Disk.</span></span> <span data-ttu-id="f2165-396">В приведенном выше примере hello, это *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="f2165-396">In hello example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a><span data-ttu-id="f2165-397">Toobe виртуального жесткого диска для диска данных присоединенного toonew экземпляры виртуальной Машины Azure</span><span class="sxs-lookup"><span data-stu-id="f2165-397">Data disk VHD toobe attached toonew Azure VM instance(s)</span></span>
<span data-ttu-id="f2165-398">После hello диск данных виртуального жесткого диска является передачи toostorage учетной записью, зарегистрировать его в качестве диска данных Azure, чтобы он мог быть вложенного tooyour новой серии DS, серии DSv2 ряда или экземпляра виртуальной Машины Azure серии GS.</span><span class="sxs-lookup"><span data-stu-id="f2165-398">After hello data disk VHD is uploaded toostorage account, register it as an Azure Data Disk so that it can be attached tooyour new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="f2165-399">Используйте эти tooregister командлеты PowerShell вашего виртуального жесткого диска в качестве диска данных Azure.</span><span class="sxs-lookup"><span data-stu-id="f2165-399">Use these PowerShell cmdlets tooregister your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="f2165-400">Укажите полный контейнера hello URL-адрес, где виртуальный жесткий ДИСК был скопирован.</span><span class="sxs-lookup"><span data-stu-id="f2165-400">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="f2165-401">Скопируйте и сохраните hello имя для этого нового диска данных Azure.</span><span class="sxs-lookup"><span data-stu-id="f2165-401">Copy and save hello name of this new Azure Data Disk.</span></span> <span data-ttu-id="f2165-402">В приведенном выше примере hello, это *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="f2165-402">In hello example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="f2165-403">Создание виртуальной машины, поддерживающей хранилище класса Premium</span><span class="sxs-lookup"><span data-stu-id="f2165-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="f2165-404">Один раз hello образ ОС или диска ОС зарегистрированы, создать новый серии DS, серии DSv2 ряда или виртуальных Машин серии GS.</span><span class="sxs-lookup"><span data-stu-id="f2165-404">Once hello OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="f2165-405">Вы используете образ операционной системы hello или имя диска операционной системы, которое вы зарегистрировали.</span><span class="sxs-lookup"><span data-stu-id="f2165-405">You will be using hello operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="f2165-406">Выберите тип hello виртуальной Машины из уровня хранилища Premium hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-406">Select hello VM type from hello Premium Storage tier.</span></span> <span data-ttu-id="f2165-407">В приведенном ниже примере мы используем hello *Standard_DS2* размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-407">In example below, we are using hello *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="f2165-408">Обновите том, что он соответствует емкости и требований к производительности и размеры hello Azure свободного toomake размер диска hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-408">Update hello disk size toomake sure it matches your capacity and performance requirements and hello available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="f2165-409">Командлеты PowerShell выполните hello шаг за шагом ниже toocreate hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-409">Follow hello step by step PowerShell cmdlets below toocreate hello new VM.</span></span> <span data-ttu-id="f2165-410">Во-первых можно задать общие параметры hello:</span><span class="sxs-lookup"><span data-stu-id="f2165-410">First, set hello common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="f2165-411">Сначала создайте облачную службу, в которой будут размещаться новые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="f2165-412">В зависимости от вашего сценария, создайте экземпляр виртуальной Машины Azure hello из либо hello образ ОС или диска ОС, которое вы зарегистрировали.</span><span class="sxs-lookup"><span data-stu-id="f2165-412">Next, depending on your scenario, create hello Azure VM instance from either hello OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="f2165-413">Обобщенный виртуальный жесткий ДИСК операционной системы toocreate несколько экземпляров виртуальной Машины Azure</span><span class="sxs-lookup"><span data-stu-id="f2165-413">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="f2165-414">Создать один или несколько новых виртуальных Машин Azure серии DS экземпляров с помощью hello hello **образа ОС Azure** которого вы зарегистрировали.</span><span class="sxs-lookup"><span data-stu-id="f2165-414">Create hello one or more new DS Series Azure VM instances using hello **Azure OS Image** that you registered.</span></span> <span data-ttu-id="f2165-415">Укажите имя этого образа ОС в конфигурации виртуальной Машины hello, при создании новой виртуальной Машины, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f2165-415">Specify this OS Image name in hello VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="f2165-416">Уникальный виртуального жесткого диска операционной системы toocreate один экземпляр виртуальной Машины Azure</span><span class="sxs-lookup"><span data-stu-id="f2165-416">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="f2165-417">Создание нового доменных служб Active Directory виртуальной Машины Azure экземпляра ряда с помощью hello **диска ОС Azure** которого вы зарегистрировали.</span><span class="sxs-lookup"><span data-stu-id="f2165-417">Create a new DS series Azure VM instance using hello **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="f2165-418">Укажите имя этого диска ОС в конфигурации виртуальной Машины hello при создании hello новой виртуальной Машины, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f2165-418">Specify this OS Disk name in hello VM configuration when creating hello new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="f2165-419">Укажите другие сведения о виртуальной машине Azure, например: облачную службу, регион, учетную запись хранения, группу доступности и политику кэширования.</span><span class="sxs-lookup"><span data-stu-id="f2165-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="f2165-420">Заметьте, что экземпляр виртуальной Машины hello должна быть совмещена с операционной системой, или диски с данными, поэтому hello выбран облачной службы, регион и учетную запись хранилища должен быть в hello местоположения hello базовые виртуальные жесткие диски таких дисков.</span><span class="sxs-lookup"><span data-stu-id="f2165-420">Note that hello VM instance must be co-located with associated operating system or data disks, so hello selected cloud service, region and storage account must all be in hello same location as hello underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="f2165-421">Присоединение диска данных</span><span class="sxs-lookup"><span data-stu-id="f2165-421">Attach data disk</span></span>
<span data-ttu-id="f2165-422">Наконец, если вы зарегистрировали данных диск VHD, присоедините их toohello нового хранилище Premium поддерживает виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="f2165-422">Lastly, if you have registered data disk VHDs, attach them toohello new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="f2165-423">Использовать следующий PowerShell командлет tooattach данных диска toohello новой виртуальной Машины и укажите hello политика кэширования.</span><span class="sxs-lookup"><span data-stu-id="f2165-423">Use following PowerShell cmdlet tooattach data disk toohello new VM and specify hello caching policy.</span></span> <span data-ttu-id="f2165-424">В примере ниже hello политика кэширования задается слишком*ReadOnly*.</span><span class="sxs-lookup"><span data-stu-id="f2165-424">In example below hello caching policy is set too*ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="f2165-425">Может быть toosupport необходимые дополнительные действия приложения, не будут рассмотрены в данном руководстве.</span><span class="sxs-lookup"><span data-stu-id="f2165-425">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="f2165-426">Проверка и планирование резервного копирования</span><span class="sxs-lookup"><span data-stu-id="f2165-426">Checking and plan backup</span></span>
<span data-ttu-id="f2165-427">Один раз приветствия работает Новая виртуальная машина запущена, доступ с помощью hello же идентификатор входа и пароль как hello исходной виртуальной Машины и убедитесь, что все работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="f2165-427">Once hello new VM is up and running, access it using hello same login id and password is as hello original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="f2165-428">Все настройки hello, включая hello чередующимися томами, может присутствовать в hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-428">All hello settings, including hello striped volumes, would be present in hello new VM.</span></span>

<span data-ttu-id="f2165-429">Последний шаг Hello — tooplan расписание резервного копирования и обслуживания для новой виртуальной Машины в зависимости от потребностей приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-429">hello last step is tooplan backup and maintenance schedule for hello new VM based on hello application's needs.</span></span>

### <span data-ttu-id="f2165-430"><a name="a-sample-migration-script"></a>Пример скрипта переноса</span><span class="sxs-lookup"><span data-stu-id="f2165-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="f2165-431">При наличии нескольких виртуальных машин toomigrate пригодятся автоматизации с помощью сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2165-431">If you have multiple VMs toomigrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="f2165-432">Ниже приведен пример сценария, который автоматизирует процесс миграции hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-432">Following is a sample script that automates hello migration of a VM.</span></span> <span data-ttu-id="f2165-433">Обратите внимание, ниже сценарий — пример и существуют некоторые предположения о hello текущего дисков виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-433">Note that below script is only an example, and there are few assumptions made about hello current VM disks.</span></span> <span data-ttu-id="f2165-434">Может потребоваться сценарий toomatch tooupdate hello с конкретного сценария.</span><span class="sxs-lookup"><span data-stu-id="f2165-434">You may need tooupdate hello script toomatch with your specific scenario.</span></span>

<span data-ttu-id="f2165-435">допущения Hello являются:</span><span class="sxs-lookup"><span data-stu-id="f2165-435">hello assumptions are:</span></span>

* <span data-ttu-id="f2165-436">Вы создаете классическую виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="f2165-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="f2165-437">Исходные диски операционной системы и диски данных находятся в одной учетной записи хранения и одном контейнере.</span><span class="sxs-lookup"><span data-stu-id="f2165-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="f2165-438">Если диски ОС и диски с данными не находятся в hello же поместить, можно использовать AzCopy или Azure PowerShell toocopy виртуальные жесткие диски по контейнеров и учетных записей хранилища.</span><span class="sxs-lookup"><span data-stu-id="f2165-438">If your OS Disks and Data Disks are not in hello same place, you can use AzCopy or Azure PowerShell toocopy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="f2165-439">См. предыдущий шаг toohello: [копирования VHD с помощью AzCopy или PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="f2165-439">Refer toohello previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="f2165-440">Редактирование toomeet этот скрипт сценария является выбор другого, но мы рекомендуем использовать AzCopy или PowerShell, так как это проще и быстрее.</span><span class="sxs-lookup"><span data-stu-id="f2165-440">Editing this script toomeet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="f2165-441">сценарий автоматизации Hello приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="f2165-441">hello automation script is provided below.</span></span> <span data-ttu-id="f2165-442">Замените текст своими данными и обновляют toomatch сценария hello конкретного сценария.</span><span class="sxs-lookup"><span data-stu-id="f2165-442">Replace text with your information and update hello script toomatch with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="f2165-443">С помощью существующего скрипта hello не сохраняет hello сетевая конфигурация источника данных виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f2165-443">Using hello existing script does not preserve hello network configuration of your source VM.</span></span> <span data-ttu-id="f2165-444">Вам потребуется toore-config hello сетевых параметров на перенесенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f2165-444">You will need toore-config hello networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
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


    #Check hello Azure PowerShell module version
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
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
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
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
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
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="f2165-445"><a name="optimization"></a>Оптимизация</span><span class="sxs-lookup"><span data-stu-id="f2165-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="f2165-446">Можно настроить конфигурацию виртуальной Машины специально toowork с стандартные диски.</span><span class="sxs-lookup"><span data-stu-id="f2165-446">Your current VM configuration may be customized specifically toowork well with Standard disks.</span></span> <span data-ttu-id="f2165-447">Например tooincrease hello производительности с помощью много дисков в чередующемся томе.</span><span class="sxs-lookup"><span data-stu-id="f2165-447">For instance, tooincrease hello performance by using many disks in a striped volume.</span></span> <span data-ttu-id="f2165-448">Например вместо 4 диска отдельно в хранилище класса Premium, может быть стоимость hello может toooptimize наличием одного диска.</span><span class="sxs-lookup"><span data-stu-id="f2165-448">For example, instead of using 4 disks separately on Premium Storage, you may be able toooptimize hello cost by having a single disk.</span></span> <span data-ttu-id="f2165-449">Оптимизация, например это toobe необходимость обрабатываются на индивидуальной основе и требуются пользовательские действия после миграции hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-449">Optimizations like this need toobe handled on a case by case basis and require custom steps after hello migration.</span></span> <span data-ttu-id="f2165-450">Кроме того Обратите внимание, что этот процесс может хорошо работать для баз данных и приложений, зависящих от разметка диска hello, определенные в программе установки hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-450">Also, note that this process may not well work for databases and applications that depend on hello disk layout defined in hello setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="f2165-451">Подготовка</span><span class="sxs-lookup"><span data-stu-id="f2165-451">Preparation</span></span>
1. <span data-ttu-id="f2165-452">Полный hello простой миграции, как описано в hello в разделе.</span><span class="sxs-lookup"><span data-stu-id="f2165-452">Complete hello Simple Migration as described in hello earlier section.</span></span> <span data-ttu-id="f2165-453">Оптимизация выполняется на hello новой виртуальной Машине после миграции hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-453">Optimizations will be performed on hello new VM after hello migration.</span></span>
2. <span data-ttu-id="f2165-454">Определите размеры дисков новый hello, необходимый для настройки оптимизации hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-454">Define hello new disk sizes needed for hello optimized configuration.</span></span>
3. <span data-ttu-id="f2165-455">Определите сопоставление спецификаций hello текущего дисков или томов toohello новый диск.</span><span class="sxs-lookup"><span data-stu-id="f2165-455">Determine mapping of hello current disks/volumes toohello new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="f2165-456">Шаги выполнения</span><span class="sxs-lookup"><span data-stu-id="f2165-456">Execution steps</span></span>
1. <span data-ttu-id="f2165-457">Создайте новые диски hello hello соответствующего размера на hello ВМ хранилища Premium.</span><span class="sxs-lookup"><span data-stu-id="f2165-457">Create hello new disks with hello right sizes on hello Premium Storage VM.</span></span>
2. <span data-ttu-id="f2165-458">Имя входа toohello ВМ и скопируйте hello данные hello текущего тома toohello нового диска, который сопоставляет toothat тома.</span><span class="sxs-lookup"><span data-stu-id="f2165-458">Login toohello VM and copy hello data from hello current volume toohello new disk that maps toothat volume.</span></span> <span data-ttu-id="f2165-459">Сделайте это для всех hello текущих томов, требующих toomap tooa новый диск.</span><span class="sxs-lookup"><span data-stu-id="f2165-459">Do this for all hello current volumes that need toomap tooa new disk.</span></span>
3. <span data-ttu-id="f2165-460">Затем измените hello приложения параметры tooswitch toohello новых дисков и отсоединение hello старых томов.</span><span class="sxs-lookup"><span data-stu-id="f2165-460">Next, change hello application settings tooswitch toohello new disks, and detach hello old volumes.</span></span>

<span data-ttu-id="f2165-461">Помощник по настройке приложения hello для повышения производительности диска, можно найти слишком[оптимизация производительности приложений](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="f2165-461">For tuning hello application for better disk performance, please refer too[Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="f2165-462">Перенос приложений</span><span class="sxs-lookup"><span data-stu-id="f2165-462">Application migrations</span></span>
<span data-ttu-id="f2165-463">Базы данных и других сложных приложений может потребоваться особые действия в соответствии с определением поставщика приложения hello hello миграции.</span><span class="sxs-lookup"><span data-stu-id="f2165-463">Databases and other complex applications may require special steps as defined by hello application provider for hello migration.</span></span> <span data-ttu-id="f2165-464">См. документацию toorespective приложения.</span><span class="sxs-lookup"><span data-stu-id="f2165-464">Please refer toorespective application documentation.</span></span> <span data-ttu-id="f2165-465">Например: </span><span class="sxs-lookup"><span data-stu-id="f2165-465">E.g.</span></span> <span data-ttu-id="f2165-466">обычно базы данных можно переносить путем резервного копирования и восстановления.</span><span class="sxs-lookup"><span data-stu-id="f2165-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2165-467">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f2165-467">Next steps</span></span>
<span data-ttu-id="f2165-468">См. следующие ресурсы для конкретных сценариев для автоматической миграции виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="f2165-468">See hello following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="f2165-469">Перенос виртуальных машин Azure между учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="f2165-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="f2165-470">Создание и отправка tooAzure виртуального жесткого диска Windows Server.</span><span class="sxs-lookup"><span data-stu-id="f2165-470">Create and upload a Windows Server VHD tooAzure.</span></span>](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="f2165-471">Создание и загрузка виртуального жесткого диска, который содержит hello операционной системы Linux</span><span class="sxs-lookup"><span data-stu-id="f2165-471">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="f2165-472">Перенос виртуальных машин из Amazon AWS tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="f2165-472">Migrating Virtual Machines from Amazon AWS tooMicrosoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="f2165-473">Кроме того см. следующие ресурсы toolearn Дополнительные сведения о хранилище Azure и виртуальных машин Azure hello:</span><span class="sxs-lookup"><span data-stu-id="f2165-473">Also, see hello following resources toolearn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="f2165-474">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="f2165-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="f2165-475">Виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="f2165-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="f2165-476">Хранилище Premium: высокопроизводительное хранилище для рабочих нагрузок виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="f2165-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
