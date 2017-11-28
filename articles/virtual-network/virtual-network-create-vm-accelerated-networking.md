---
title: "виртуальной машине Azure с помощью Accelerated сетевых aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate виртуальную машину с Accelerated работа по сети."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="02e7e-103">Создание виртуальной машины с ускоренной сетью</span><span class="sxs-lookup"><span data-stu-id="02e7e-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="02e7e-104">В этом учебнике вы узнаете, как toocreate виртуальной машины (ВМ) Azure с Accelerated работа по сети.</span><span class="sxs-lookup"><span data-stu-id="02e7e-104">In this tutorial, you learn how toocreate an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="02e7e-105">Ускорение работы в сети — общедоступно для Windows и для определенных дистрибутивов Linux (общедоступная предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="02e7e-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="02e7e-106">Ускорение сеть позволяет tooa виртуализацию SR-IOV один корневой ввода-вывода виртуальной Машины, значительно повышает его производительность сети.</span><span class="sxs-lookup"><span data-stu-id="02e7e-106">Accelerated networking enables single root I/O virtualization (SR-IOV) tooa VM, greatly improving its networking performance.</span></span> <span data-ttu-id="02e7e-107">Этот путь высокой производительности обходит hello узла из пути к данным hello, уменьшение задержки, флуктуации и использования ЦП, для использования с hello наиболее ресурсоемких рабочих нагрузок сети на поддерживаемых типов ВМ.</span><span class="sxs-lookup"><span data-stu-id="02e7e-107">This high-performance path bypasses hello host from hello datapath reducing latency, jitter, and CPU utilization, for use with hello most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="02e7e-108">Следующий рисунок показывает связи между две виртуальные машины (VM) с и без поддержки сети ускорителем Hello:</span><span class="sxs-lookup"><span data-stu-id="02e7e-108">hello following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![Сравнение](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="02e7e-110">Без поддержки ускорителем сети все сетевого трафика и из него hello ВМ необходимо проходить по hello узла и виртуального коммутатора hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-110">Without accelerated networking, all networking traffic in and out of hello VM must traverse hello host and hello virtual switch.</span></span> <span data-ttu-id="02e7e-111">Hello виртуальный коммутатор предоставляет все применение политики, такой как сетевых групп безопасности, доступ к данным списков управления, изоляции и другой трафик toonetwork службы виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="02e7e-111">hello virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services toonetwork traffic.</span></span> <span data-ttu-id="02e7e-112">Дополнительные сведения о виртуальных коммутаторов, чтение hello toolearn [виртуализации сети Hyper-V и виртуального коммутатора](https://technet.microsoft.com/library/jj945275.aspx) статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-112">toolearn more about virtual switches, read hello [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="02e7e-113">С ускорителем сетями сетевой трафик поступает на виртуальной Машине hello сетевого интерфейса (NIC) и пересылаются toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="02e7e-113">With accelerated networking, network traffic arrives at hello VM's network interface (NIC), and is then forwarded toohello VM.</span></span> <span data-ttu-id="02e7e-114">Все сетевые политики, которые hello виртуального коммутатора применяется без ускорителем сети являются прямой и применяется в оборудовании.</span><span class="sxs-lookup"><span data-stu-id="02e7e-114">All network policies that hello virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="02e7e-115">Применение политики в оборудования позволяет hello Сетевых tooforward сетевой трафик непосредственно toohello ВМ, минуя hello узла и виртуального коммутатора hello, сохраняя все hello политику, которую он применяется в узле hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-115">Applying policy in hardware enables hello NIC tooforward network traffic directly toohello VM, bypassing hello host and hello virtual switch, while maintaining all hello policy it applied in hello host.</span></span>

<span data-ttu-id="02e7e-116">Hello преимущества ускорителем сети применяются только toohello виртуальной Машине, которая была включена.</span><span class="sxs-lookup"><span data-stu-id="02e7e-116">hello benefits of accelerated networking only apply toohello VM that it is enabled on.</span></span> <span data-ttu-id="02e7e-117">Для получения наилучших результатов hello это идеальный tooenable этой функции для по крайней мере две виртуальные машины подключены toohello одной виртуальной сети Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="02e7e-117">For hello best results, it is ideal tooenable this feature on at least two VMs connected toohello same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="02e7e-118">При обмене данными между виртуальными сетями или подключении в локальной, эта функция имеет минимальное влияние toooverall задержку.</span><span class="sxs-lookup"><span data-stu-id="02e7e-118">When communicating across VNets or connecting on-premises, this feature has minimal impact toooverall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="02e7e-119">Это Linux общедоступной предварительной версии не может иметь одинаковый уровень доступности и надежности, как и в случае функций, которые hello в целом общедоступный выпуск.</span><span class="sxs-lookup"><span data-stu-id="02e7e-119">This Linux Public Preview may not have hello same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="02e7e-120">функция Hello не поддерживается, могут ограничены возможности и могут быть доступны не во всех расположений в Azure.</span><span class="sxs-lookup"><span data-stu-id="02e7e-120">hello feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="02e7e-121">Hello последних уведомлений на доступность и состояние этой функцией проверьте страницу обновления виртуальной сети Azure hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-121">For hello most up-to-date notifications on availability and status of this feature, check hello Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="02e7e-122">Преимущества</span><span class="sxs-lookup"><span data-stu-id="02e7e-122">Benefits</span></span>
* <span data-ttu-id="02e7e-123">**Более низкая задержка или более поздней версии пакетов в секунду (pps):** удаление hello виртуальный коммутатор из пути к данным hello удаляет hello время, затрачиваемое пакетов в узле hello для обработки политики и увеличения hello число пакетов, которые могут быть обработаны внутри hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="02e7e-123">**Lower Latency / Higher packets per second (pps):** Removing hello virtual switch from hello datapath removes hello time packets spend in hello host for policy processing and increases hello number of packets that can be processed inside hello VM.</span></span>
* <span data-ttu-id="02e7e-124">**Сокращение флуктуации:** виртуальный коммутатор обработки зависит от hello объем политики, которая требует применения toobe и hello нагрузки hello ЦП, осуществляющего hello обработки.</span><span class="sxs-lookup"><span data-stu-id="02e7e-124">**Reduced jitter:** Virtual switch processing depends on hello amount of policy that needs toobe applied and hello workload of hello CPU that is doing hello processing.</span></span> <span data-ttu-id="02e7e-125">Разгрузки оборудования toohello принудительного применения политики hello устраняет этой изменчивостью, доставку пакетов напрямую toohello ВМ, удаление связи с узлом tooVM hello и все программное обеспечение прерываний и контекст переключается.</span><span class="sxs-lookup"><span data-stu-id="02e7e-125">Offloading hello policy enforcement toohello hardware removes that variability by delivering packets directly toohello VM, removing hello host tooVM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="02e7e-126">**Уменьшается загрузка ЦП:** обход hello виртуальный коммутатор в узле hello ведет сборки ЦП для обработки сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="02e7e-126">**Decreased CPU utilization:** Bypassing hello virtual switch in hello host leads tooless CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="02e7e-127"><a name="Limitations"></a>Ограничения</span><span class="sxs-lookup"><span data-stu-id="02e7e-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="02e7e-128">При использовании этой возможности действуют следующие ограничения Hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-128">hello following limitations exist when using this capability:</span></span>

* <span data-ttu-id="02e7e-129">**Создание сетевого интерфейса.** Функцию ускорения сети можно включить только в новом сетевом интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="02e7e-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="02e7e-130">Ее нельзя включить в имеющемся сетевом интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="02e7e-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="02e7e-131">**Создание виртуальной Машины:** сетевого Адаптера с ускорителем сеть включенная может только вложенные tooa виртуальной Машины при hello виртуальной Машины создать.</span><span class="sxs-lookup"><span data-stu-id="02e7e-131">**VM creation:** A NIC with accelerated networking enabled can only be attached tooa VM when hello VM is created.</span></span> <span data-ttu-id="02e7e-132">Hello сетевого Адаптера не может быть вложенного tooan существующей виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="02e7e-132">hello NIC cannot be attached tooan existing VM.</span></span>
* <span data-ttu-id="02e7e-133">**Регионы.** Виртуальные машины Windows с ускоренной сетью доступны в большинстве регионов Azure,</span><span class="sxs-lookup"><span data-stu-id="02e7e-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="02e7e-134">Виртуальные машины Linux с ускоренной сетью доступны в нескольких регионах.</span><span class="sxs-lookup"><span data-stu-id="02e7e-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="02e7e-135">Hello областей, которые эта возможность доступна в расширение.</span><span class="sxs-lookup"><span data-stu-id="02e7e-135">hello regions this capability is available in is expanding.</span></span> <span data-ttu-id="02e7e-136">См. в разделе блога обновления виртуальной сети Azure hello ниже для получения последних сведений hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-136">Please see hello Azure Virtual Networking Updates blog below for hello latest information.</span></span>   
* <span data-ttu-id="02e7e-137">**Поддерживаемые операционные системы.** Windows: Microsoft Windows Server 2012 R2 Datacenter и Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="02e7e-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="02e7e-138">Linux: Ubuntu Server 16.04 LTS с ядром 4.4.0-77 или более поздней версии, SLES 12 SP2, RHEL 7.3 и CentOS 7.3 (опубликована Rogue Wave Software).</span><span class="sxs-lookup"><span data-stu-id="02e7e-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="02e7e-139">**Размер виртуальной машины.** Экземпляры общего назначения и оптимизированные для вычислений экземпляры с минимум восемью ядрами.</span><span class="sxs-lookup"><span data-stu-id="02e7e-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="02e7e-140">Дополнительные сведения см. в разделе hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) и [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) статьи размеров виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="02e7e-140">For more information, see hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="02e7e-141">Hello набор поддерживаемых размеров экземпляр виртуальной Машины будет расширяться в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-141">hello set of supported VM instance sizes will expand in hello future.</span></span>
* <span data-ttu-id="02e7e-142">**Развертывание только с помощью Azure Resource Manager (ARM).** Ускоренная сеть недоступна для развертывания с помощью ASM/RDFE.</span><span class="sxs-lookup"><span data-stu-id="02e7e-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="02e7e-143">Изменения ограничения toothese объявляются через hello [виртуальную сеть Azure обновляет](https://azure.microsoft.com/updates/accelerated-networking-in-preview) страницы.</span><span class="sxs-lookup"><span data-stu-id="02e7e-143">Changes toothese limitations are announced through hello [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="02e7e-144">Создание виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="02e7e-144">Create a Windows VM</span></span>
<span data-ttu-id="02e7e-145">Вы можете использовать hello портал Azure или Azure [PowerShell](#windows-powershell) toocreate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="02e7e-145">You can use hello Azure portal or Azure [PowerShell](#windows-powershell) toocreate hello VM.</span></span>

### <span data-ttu-id="02e7e-146"><a name="windows-portal"></a>Портал</span><span class="sxs-lookup"><span data-stu-id="02e7e-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="02e7e-147">Откройте веб-браузер, hello Azure [портала](https://portal.azure.com) и выполните вход с помощью Azure [учетной записи](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="02e7e-147">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="02e7e-148">Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="02e7e-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="02e7e-149">На портале hello щелкните **+ создать** > **вычислений** > **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="02e7e-149">In hello portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="02e7e-150">В hello **Windows Server 2016 Datacenter** колонки, отображается, оставьте *диспетчера ресурсов* выбранных в разделе **выберите модель развертывания**и нажмите кнопку **создать** .</span><span class="sxs-lookup"><span data-stu-id="02e7e-150">In hello **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="02e7e-151">В hello **основы** колонки, отображается, введите следующие значения hello оставьте hello оставшиеся параметры по умолчанию или выбрать или ввести собственные значения и щелкните hello **ОК** кнопки:</span><span class="sxs-lookup"><span data-stu-id="02e7e-151">In hello **Basics** blade that appears, enter hello following values, leave hello remaining default options or select or enter your own values, and click hello **OK** button:</span></span>

    |<span data-ttu-id="02e7e-152">Настройка</span><span class="sxs-lookup"><span data-stu-id="02e7e-152">Setting</span></span>|<span data-ttu-id="02e7e-153">Значение</span><span class="sxs-lookup"><span data-stu-id="02e7e-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="02e7e-154">Имя</span><span class="sxs-lookup"><span data-stu-id="02e7e-154">Name</span></span>|<span data-ttu-id="02e7e-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="02e7e-155">MyVm</span></span>|
    |<span data-ttu-id="02e7e-156">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="02e7e-156">Resource group</span></span>|<span data-ttu-id="02e7e-157">Выберите **Создать** и введите *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="02e7e-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="02e7e-158">Расположение</span><span class="sxs-lookup"><span data-stu-id="02e7e-158">Location</span></span>|<span data-ttu-id="02e7e-159">Западная часть США 2</span><span class="sxs-lookup"><span data-stu-id="02e7e-159">West US 2</span></span>|

    <span data-ttu-id="02e7e-160">Если вы новый tooAzure, Дополнительные сведения о [групп ресурсов](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [подписки](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), и [расположения](https://azure.microsoft.com/regions) (они также называется tooas областей).</span><span class="sxs-lookup"><span data-stu-id="02e7e-160">If you're new tooAzure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred tooas regions).</span></span>
5. <span data-ttu-id="02e7e-161">В hello **выберите размер** колонки, которое откроется, введите *8* в hello **ядер менее** , а затем нажмите кнопку **просмотреть все**.</span><span class="sxs-lookup"><span data-stu-id="02e7e-161">In hello **Choose a size** blade that appears, enter *8* in hello **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="02e7e-162">Нажмите кнопку **DS4_V2 Стандартная**, или любой поддерживаемый виртуальной Машины, нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="02e7e-162">Click **DS4_V2 Standard**, or any supported VM, then click hello **Select** button.</span></span>
7. <span data-ttu-id="02e7e-163">В hello **параметры** колонки, отображается, оставьте все параметры, как-является, за исключением того, щелкните **включено** под **Accelerated сети**, нажмите кнопку hello **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="02e7e-163">In hello **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click hello **OK** button.</span></span> <span data-ttu-id="02e7e-164">**Примечание:** , если в предыдущих шагах был выбран значения для размера виртуальной Машины, операционной системы или расположение, не перечисленным в hello [ограничения](#Limitations) данной статьи **сети Accelerated**не отображается.</span><span class="sxs-lookup"><span data-stu-id="02e7e-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in hello [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="02e7e-165">В hello **Сводка** колонки, отображается, щелкните hello **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="02e7e-165">In hello **Summary** blade that appears, click hello **OK** button.</span></span> <span data-ttu-id="02e7e-166">Azure запускает создание hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="02e7e-166">Azure starts creating hello VM.</span></span> <span data-ttu-id="02e7e-167">Этот процесс займет несколько минут.</span><span class="sxs-lookup"><span data-stu-id="02e7e-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="02e7e-168">tooinstall hello ускорением сетевой драйвер для Windows, hello завершения шагов в hello [настроить Windows](#configure-windows) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-168">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="02e7e-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="02e7e-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="02e7e-170">Установите последнюю версию Azure PowerShell hello hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модуля.</span><span class="sxs-lookup"><span data-stu-id="02e7e-170">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="02e7e-171">Если вы новый tooAzure PowerShell чтения hello [Обзор Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-171">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="02e7e-172">Запустите сеанс PowerShell, нажав кнопку Пуск Windows hello, введя **powershell**, выбрав **PowerShell** из результатов поиска hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-172">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="02e7e-173">В окне PowerShell, введите hello `login-azurermaccount` toosign команда с помощью Azure [учетной записи](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="02e7e-173">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="02e7e-174">Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="02e7e-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="02e7e-175">В браузере скопируйте hello следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="02e7e-175">In your browser, copy hello following script:</span></span>
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="02e7e-176">В окне PowerShell щелкните правой кнопкой мыши сценарий toopaste hello и запустить его выполнения.</span><span class="sxs-lookup"><span data-stu-id="02e7e-176">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="02e7e-177">Появится запрос на ввод имени пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="02e7e-177">You are prompted for a username and password.</span></span> <span data-ttu-id="02e7e-178">Используйте эти учетные данные toolog в toohello виртуальной Машины при подключении tooit в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-178">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="02e7e-179">Если вы изменили значения в сценарии hello перед его выполнением сбоя сценария hello, подтвердите hello значения используются для размера виртуальной Машины, операционной системы и расположение, перечислены в hello [ограничения](#Limitations) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-179">If hello script fails, and you changed values in hello script before executing it, confirm hello values you used for VM size, operating system, and location are listed in hello [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="02e7e-180">tooinstall hello ускорением сетевой драйвер для Windows, hello завершения шагов в hello [настроить Windows](#configure-windows) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-180">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="02e7e-181"><a name="configure-windows"></a>Настройка виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="02e7e-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="02e7e-182">После создания hello ВМ в Azure, необходимо установить hello ускорителем сетевой драйвер для Windows.</span><span class="sxs-lookup"><span data-stu-id="02e7e-182">Once you create hello VM in Azure, you must install hello accelerated networking driver for Windows.</span></span> <span data-ttu-id="02e7e-183">Перед завершением hello, выполнив действия, необходимо создать виртуальную Машину Windows с ускорителем сети, с помощью либо hello [портала](#windows-portal) или [PowerShell](#windows-powershell) шаги в этой статье.</span><span class="sxs-lookup"><span data-stu-id="02e7e-183">Before completing hello following steps, you must have created a Windows VM with accelerated networking using either hello [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="02e7e-184">Откройте веб-браузер, hello Azure [портала](https://portal.azure.com) и выполните вход с помощью Azure [учетной записи](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="02e7e-184">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="02e7e-185">Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="02e7e-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="02e7e-186">В поле hello, содержащее текст hello *Найдите ресурсы* вверху hello hello портал Azure, введите *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="02e7e-186">In hello box that contains hello text *Search resources* at hello top of hello Azure portal, type *MyVm*.</span></span> <span data-ttu-id="02e7e-187">Когда **MyVm** появится в результатах поиска hello, щелкните его.</span><span class="sxs-lookup"><span data-stu-id="02e7e-187">When **MyVm** appears in hello search results, click it.</span></span>
3. <span data-ttu-id="02e7e-188">В hello **MyVm** колонки, отображается, щелкните hello **Connect** кнопка в верхнем левом углу hello колонка hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-188">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="02e7e-189">**Примечание:** Если **создание** отображается в группе hello **Connect** кнопки, Azure не завершено создание hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="02e7e-189">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="02e7e-190">Нажмите кнопку **Connect** только в том случае, если больше нет **создание** под hello **Connect** кнопки.</span><span class="sxs-lookup"><span data-stu-id="02e7e-190">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
4. <span data-ttu-id="02e7e-191">Разрешить hello toodownload ваш браузер **MyVm.rdp** файла.</span><span class="sxs-lookup"><span data-stu-id="02e7e-191">Allow your browser toodownload hello **MyVm.rdp** file.</span></span>  <span data-ttu-id="02e7e-192">После загрузки, выберите файл tooopen hello его.</span><span class="sxs-lookup"><span data-stu-id="02e7e-192">Once downloaded, click hello file tooopen it.</span></span> 
5. <span data-ttu-id="02e7e-193">Нажмите кнопку hello **Connect** кнопку в hello **удаленный рабочий стол** поле, которое появляется уведомление о том, что hello не удается определить издателя удаленного подключения hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-193">Click hello **Connect** button in hello **Remote Desktop Connection** box that appears, notifying you that hello publisher of hello remote connection can't be identified.</span></span>
6. <span data-ttu-id="02e7e-194">В hello **безопасности Windows** щелкните поле, которое появляется, **Дополнительные варианты**, нажмите кнопку **использовать другую учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="02e7e-194">In hello **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="02e7e-195">Введите hello имя пользователя и пароль, указанный на шаге 4, а затем нажмите кнопку hello **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="02e7e-195">Enter hello username and password you entered in step 4, then click hello **OK** button.</span></span>
7. <span data-ttu-id="02e7e-196">Нажмите кнопку hello **Да** кнопку в поле удаленный рабочий стол hello, появится уведомление о невозможности проверки удостоверения hello hello удаленного компьютера.</span><span class="sxs-lookup"><span data-stu-id="02e7e-196">Click hello **Yes** button in hello Remote Desktop Connection box that appears, notifying you that hello identity of hello remote computer cannot be verified.</span></span>
8. <span data-ttu-id="02e7e-197">Щелкните правой кнопкой мыши кнопку Пуск Windows hello и нажмите кнопку **устройства**.</span><span class="sxs-lookup"><span data-stu-id="02e7e-197">Right-click hello Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="02e7e-198">Разверните hello **сетевые адаптеры** узла.</span><span class="sxs-lookup"><span data-stu-id="02e7e-198">Expand hello **Network adapters** node.</span></span> <span data-ttu-id="02e7e-199">Убедитесь, что hello **Mellanox ConnectX-3 виртуальный адаптер Ethernet функция** появляется, как показано в следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="02e7e-199">Confirm that hello **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in hello following picture:</span></span>
   
    ![Диспетчер устройств](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="02e7e-201">Ускорение работы в сети теперь включено на вашей виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="02e7e-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="02e7e-202">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="02e7e-202">Create a Linux VM</span></span>
<span data-ttu-id="02e7e-203">Вы можете использовать hello портал Azure или Azure [PowerShell](#linux-powershell) toocreate Ubuntu или SLES виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="02e7e-203">You can use hello Azure portal or Azure [PowerShell](#linux-powershell) toocreate an Ubuntu or SLES VM.</span></span> <span data-ttu-id="02e7e-204">У виртуальных машин RHEL и CentOS другой рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="02e7e-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="02e7e-205">См. в разделе hello приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="02e7e-205">Please see hello instructions below.</span></span>

### <span data-ttu-id="02e7e-206"><a name="linux-portal"></a>Портал</span><span class="sxs-lookup"><span data-stu-id="02e7e-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="02e7e-207">Регистрация для hello accelerated сети для предварительной версии Linux, выполнив шаги 1 – 5 hello [создайте виртуальную Машину Linux — PowerShell](#linux-powershell) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-207">Register for hello accelerated networking for Linux preview by completing steps 1-5 of hello [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="02e7e-208">Не удается зарегистрировать hello предварительную версию портала hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-208">You cannot register for hello preview in hello portal.</span></span>
2. <span data-ttu-id="02e7e-209">Выполните действия 1 – 8 в hello [создания виртуальной Машины Windows - портал](#windows-portal) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-209">Complete steps 1-8 in hello [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="02e7e-210">На шаге 2 выберите **Ubuntu Server 16.04 LTS**, а не **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="02e7e-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="02e7e-211">В этом учебнике выберите toouse пароль, а не ключ SSH на то, что для рабочих развертываний можно использовать.</span><span class="sxs-lookup"><span data-stu-id="02e7e-211">For this tutorial, choose toouse a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="02e7e-212">Если **Accelerated сети** не отображается, когда шаги 7 hello [создания виртуальной Машины Windows - портал](#windows-portal) разделе данной статьи, вполне вероятно, по одной из следующих причин hello:</span><span class="sxs-lookup"><span data-stu-id="02e7e-212">If **Accelerated networking** does not appear when you complete step 7 of hello [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of hello following reasons:</span></span>
    - <span data-ttu-id="02e7e-213">Вы еще не зарегистрированы для предварительного просмотра hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-213">You are not yet registered for hello preview.</span></span> <span data-ttu-id="02e7e-214">Убедитесь, что состояние регистрации **зарегистрированные**, как описано в шаге 4 hello [создайте виртуальную Машину Linux — Powershell](#linux-powershell) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-214">Confirm that your registration state is **Registered**, as explained in step 4 of hello [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="02e7e-215">**Примечание:** Если участвовали в hello Accelerated сети для виртуальных машин Windows preview (его нет больше необходимости tooregister toouse Accelerated сети для виртуальных машин Windows), вы не зарегистрированы автоматически hello Accelerated сети для Просмотр виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="02e7e-215">**Note:** If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="02e7e-216">Необходимо зарегистрировать для hello Accelerated сети для виртуальных машин Linux предварительного просмотра tooparticipate в нем.</span><span class="sxs-lookup"><span data-stu-id="02e7e-216">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
    - <span data-ttu-id="02e7e-217">Вы не выбрали размер виртуальной Машины, операционной системы или папке, заданной в hello [ограничения](#limitations) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-217">You have not selected a VM size, operating system, or location listed in hello [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="02e7e-218">tooinstall hello ускорением сетевой драйвер для Linux, hello завершения шагов в hello [Настройка Linux](#configure-linux) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-218">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="02e7e-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="02e7e-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="02e7e-220">При создании виртуальных машин Linux с ускорителем сетями в подписке и повторить попытку toocreate виртуальной Машины Windows с ускорителем сетевых технологий в hello одной подписке, hello Создание виртуальной Машины Windows может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="02e7e-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt toocreate a Windows VM with accelerated networking in hello same subscription, hello Windows VM creation may fail.</span></span> <span data-ttu-id="02e7e-221">Во время действия предварительной версии мы советуем создавать виртуальные машины Windows и Linux с функцией ускорения сети в отдельных подписках.</span><span class="sxs-lookup"><span data-stu-id="02e7e-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="02e7e-222">Установите последнюю версию Azure PowerShell hello hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модуля.</span><span class="sxs-lookup"><span data-stu-id="02e7e-222">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="02e7e-223">Если вы новый tooAzure PowerShell чтения hello [Обзор Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-223">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="02e7e-224">Запустите сеанс PowerShell, нажав кнопку Пуск Windows hello, введя **powershell**, выбрав **PowerShell** из результатов поиска hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-224">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="02e7e-225">В окне PowerShell, введите hello `login-azurermaccount` toosign команда с помощью Azure [учетной записи](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="02e7e-225">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="02e7e-226">Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="02e7e-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="02e7e-227">Регистрация для hello accelerated сети для Azure preview, выполнив следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="02e7e-227">Register for hello accelerated networking for Azure preview by completing hello following steps:</span></span>
    - <span data-ttu-id="02e7e-228">Отправить сообщение электронной почты слишком[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) своим Идентификатором подписки Azure, а предполагаемого использования.</span><span class="sxs-lookup"><span data-stu-id="02e7e-228">Send an email too[axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="02e7e-229">Дождитесь, пока придет письмо с подтверждением от корпорации Майкрософт о том, что ваша подписка включена.</span><span class="sxs-lookup"><span data-stu-id="02e7e-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="02e7e-230">Введите следующие команды tooconfirm зарегистрированы для предварительного просмотра hello hello:</span><span class="sxs-lookup"><span data-stu-id="02e7e-230">Enter hello following command tooconfirm you are registered for hello preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="02e7e-231">Не нужно выполнять шаг 5 до **зарегистрированные** отображается в выходных данных после выполнения предыдущей команды hello hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-231">Do not continue with step 5 until **Registered** appears in hello output after you enter hello previous command.</span></span> <span data-ttu-id="02e7e-232">Выходные данные должны выглядеть следующие hello, выходные данные перед продолжением:</span><span class="sxs-lookup"><span data-stu-id="02e7e-232">Your output must look like hello following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="02e7e-233">Если вы участвовали в hello Accelerated сети для виртуальных машин Windows preview (it's нет больше необходимости tooregister toouse Accelerated сети для виртуальных машин Windows) вы не зарегистрированы автоматически hello Accelerated сети для виртуальных машин Linux предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="02e7e-233">If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="02e7e-234">Необходимо зарегистрировать для hello Accelerated сети для виртуальных машин Linux предварительного просмотра tooparticipate в нем.</span><span class="sxs-lookup"><span data-stu-id="02e7e-234">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
      >
5. <span data-ttu-id="02e7e-235">В браузере скопируйте следующий скрипт, заменив нужным Ubuntu или SLES hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-235">In your browser, copy hello following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="02e7e-236">Опять же, рабочий процесс для Redhat и CentOS разный. Он приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="02e7e-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="02e7e-237">В окне PowerShell щелкните правой кнопкой мыши сценарий toopaste hello и запустить его выполнения.</span><span class="sxs-lookup"><span data-stu-id="02e7e-237">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="02e7e-238">Появится запрос на ввод имени пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="02e7e-238">You are prompted for a username and password.</span></span> <span data-ttu-id="02e7e-239">Используйте эти учетные данные toolog в toohello виртуальной Машины при подключении tooit в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-239">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="02e7e-240">При сбое скрипта hello, убедитесь, что:</span><span class="sxs-lookup"><span data-stu-id="02e7e-240">If hello script fails, confirm that:</span></span>
    - <span data-ttu-id="02e7e-241">Вы зарегистрированы для предварительного просмотра hello, как описано в шаге 4</span><span class="sxs-lookup"><span data-stu-id="02e7e-241">You are registered for hello preview, as explained in step 4</span></span>
    - <span data-ttu-id="02e7e-242">Если вы изменили размер виртуальной Машины, тип операционной системы или расположение значений в скрипт hello перед его выполнением, что hello значения перечислены в hello [ограничения](#Limitations) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-242">If you changed VM size, operating system type, or location values in hello script before executing it, that hello values are listed in hello [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="02e7e-243">tooinstall hello ускорением сетевой драйвер для Linux, hello завершения шагов в hello [Настройка Linux](#configure-linux) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="02e7e-243">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="02e7e-244"><a name="configure-linux"></a>Настройка виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="02e7e-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="02e7e-245">После создания hello ВМ в Azure, необходимо установить сетевой драйвер hello для Linux.</span><span class="sxs-lookup"><span data-stu-id="02e7e-245">Once you create hello VM in Azure, you must install hello accelerated networking driver for Linux.</span></span> <span data-ttu-id="02e7e-246">Перед завершением hello, выполнив действия, необходимо создать виртуальную Машину Linux с ускорителем сети, с помощью либо hello [портала](#linux-portal) или [PowerShell](#linux-powershell) шаги в этой статье.</span><span class="sxs-lookup"><span data-stu-id="02e7e-246">Before completing hello following steps, you must have created a Linux VM with accelerated networking using either hello [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="02e7e-247">Откройте веб-браузер, hello Azure [портала](https://portal.azure.com) и выполните вход с помощью Azure [учетной записи](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="02e7e-247">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="02e7e-248">Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="02e7e-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="02e7e-249">Вверху hello hello портала, toohello справа от приветствия *Найдите ресурсы* панели, щелкните hello **> _** toostart значок оболочке Bash облака (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="02e7e-249">At hello top of hello portal, toohello right of hello *Search resources* bar, click hello **>_** icon toostart a Bash cloud shell (Preview).</span></span> <span data-ttu-id="02e7e-250">Hello Bash облака оболочки появится область внизу hello hello портала и через несколько секунд представляется  **username@Azure:~ $** строки.</span><span class="sxs-lookup"><span data-stu-id="02e7e-250">hello Bash cloud shell pane appears at hello bottom of hello portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="02e7e-251">На то, что вы можете toohello SSH виртуальной Машины с вашего компьютера, а не оболочки облака hello, hello инструкции в этом учебнике предполагается, что вы используете hello облака оболочки.</span><span class="sxs-lookup"><span data-stu-id="02e7e-251">Though you can SSH toohello VM from your computer, rather than hello cloud shell, hello instructions in this tutorial assume you're using hello cloud shell.</span></span>
3. <span data-ttu-id="02e7e-252">Вверху hello портала hello в hello поле, содержащее текст hello *Найдите ресурсы*, тип *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="02e7e-252">At hello top of hello portal, in hello box that contains hello text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="02e7e-253">Когда **MyVm** появится в результатах поиска hello, щелкните его.</span><span class="sxs-lookup"><span data-stu-id="02e7e-253">When **MyVm** appears in hello search results, click it.</span></span>
4. <span data-ttu-id="02e7e-254">В hello **MyVm** колонки, отображается, щелкните hello **Connect** кнопка в верхнем левом углу hello колонка hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-254">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="02e7e-255">**Примечание:** Если **создание** отображается в группе hello **Connect** кнопки, Azure не завершено создание hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="02e7e-255">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="02e7e-256">Нажмите кнопку **Connect** только в том случае, если больше нет **создание** под hello **Connect** кнопки.</span><span class="sxs-lookup"><span data-stu-id="02e7e-256">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
5. <span data-ttu-id="02e7e-257">Azure открывает окно, предлагающее tooenter hello `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="02e7e-257">Azure opens a box telling you tooenter hello `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="02e7e-258">Введите эту команду в hello облака оболочки (или копировать его из поля hello, указанную в шаг 4 и вставьте его в toohello облаке оболочки), затем нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="02e7e-258">Enter this command in hello cloud shell (or copy it from hello box that appeared in step 4 and paste it in toohello cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="02e7e-259">Ввод **Да** вопрос toohello запросом вы toocontinue подключения, затем нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="02e7e-259">Enter **yes** toohello question asking you if you want toocontinue connecting, then press Enter.</span></span>
7. <span data-ttu-id="02e7e-260">Введите пароль hello, введенное при создании hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="02e7e-260">Enter hello password you entered when creating hello VM.</span></span> <span data-ttu-id="02e7e-261">Один раз успешно выполнил вход toohello ВМ, вы видите adminuser@MyVm:~ $ запрос.</span><span class="sxs-lookup"><span data-stu-id="02e7e-261">Once successfully logged in toohello VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="02e7e-262">Вы вошли в toohello виртуальной Машине через сеанс оболочки hello облака.</span><span class="sxs-lookup"><span data-stu-id="02e7e-262">You are now logged in toohello VM through hello cloud shell session.</span></span> <span data-ttu-id="02e7e-263">**Примечание.** Срок действия сеанса Cloud Shell истекает после 10 минут бездействия.</span><span class="sxs-lookup"><span data-stu-id="02e7e-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="02e7e-264">На этом этапе инструкции hello различаются в зависимости от hello распространения, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="02e7e-264">At this point, hello instructions vary based on hello distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="02e7e-265">Ubuntu и SLES</span><span class="sxs-lookup"><span data-stu-id="02e7e-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="02e7e-266">В строке приветствия введите `uname -r` и проверить версию hello для:</span><span class="sxs-lookup"><span data-stu-id="02e7e-266">At hello prompt, enter `uname -r` and confirm hello version for:</span></span>

    * <span data-ttu-id="02e7e-267">Ubuntu — это версия 4.4.0-77-generic или более поздняя.</span><span class="sxs-lookup"><span data-stu-id="02e7e-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="02e7e-268">SLES — это версия 4.4.59-92.20-default или более поздняя.</span><span class="sxs-lookup"><span data-stu-id="02e7e-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="02e7e-269">Создайте связь между hello стандартной сети виртуального сетевого адаптера и сетевой hello accelerated виртуального сетевого адаптера с выполнением команд hello, следующие.</span><span class="sxs-lookup"><span data-stu-id="02e7e-269">Create a bond between hello standard networking vNIC and hello accelerated networking vNIC by running hello commands that follow.</span></span> <span data-ttu-id="02e7e-270">Трафик сети использует hello выше, выполняя ускорителем сети виртуального сетевого адаптера, когда связь hello гарантирует, что сетевой трафик не будет прервано по некоторые изменения в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="02e7e-270">Network traffic uses hello higher performing accelerated networking vNIC, while hello bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="02e7e-271">После выполнения скрипта hello hello виртуальная машина будет перезапущена после приостановки 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="02e7e-271">After running hello script, hello VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="02e7e-272">Один раз hello перезапуске ВМ повторно подключиться tooit, выполнив шаги 5 – 7, еще раз.</span><span class="sxs-lookup"><span data-stu-id="02e7e-272">Once hello VM is restarted, reconnect tooit by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="02e7e-273">Запустите hello `ifconfig` команды и убедитесь, что оказались bond0 hello интерфейс отображается вверх.</span><span class="sxs-lookup"><span data-stu-id="02e7e-273">Run hello `ifconfig` command and confirm that bond0 has come up and hello interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="02e7e-274">Приложения, использующие ускорителем сети должен обмениваться данными по hello *bond0* интерфейс не *eth0*.</span><span class="sxs-lookup"><span data-stu-id="02e7e-274">Applications using accelerated networking must communicate over hello *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="02e7e-275">Имя интерфейса Hello может измениться до выхода общедоступной версии ускорителем сети.</span><span class="sxs-lookup"><span data-stu-id="02e7e-275">hello interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="02e7e-276">RHEL или CentOS</span><span class="sxs-lookup"><span data-stu-id="02e7e-276">RHEL/CentOS</span></span>

<span data-ttu-id="02e7e-277">Создание виртуальной Машины CentOS 7.3 или Red Hat Enterprise Linux требуются некоторые дополнительные шаги tooload hello последние версии драйверов, необходимых для SR-IOV и hello драйвер виртуальной функции (Виртуальной) для hello сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="02e7e-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps tooload hello latest drivers needed for SR-IOV and hello Virtual Function (VF) driver for hello network card.</span></span> <span data-ttu-id="02e7e-278">Hello первый этап инструкции hello подготавливает образ, который может быть toomake используется один или несколько виртуальных машин, имеющих предварительно загрузить драйверы hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-278">hello first phase of hello instructions prepares an image that can be used toomake one or more virtual machines that have hello drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="02e7e-279">Первый этап: подготовка базового образа Red Hat Enterprise Linux или CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="02e7e-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="02e7e-280">Подготовьте виртуальную машину CentOS 7.3 без SRIOV в Azure.</span><span class="sxs-lookup"><span data-stu-id="02e7e-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="02e7e-281">Установите LIS 4.2.2:</span><span class="sxs-lookup"><span data-stu-id="02e7e-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="02e7e-282">Скачайте файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="02e7e-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="02e7e-283">Отзовите эту виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="02e7e-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="02e7e-284">Из портала Azure остановить эту виртуальную Машину; и перейдите в tooVM «диски», записи hello OSDisk URI виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="02e7e-284">From Azure portal, stop this VM; and go tooVM’s "Disks", capture hello OSDisk’s VHD URI.</span></span> <span data-ttu-id="02e7e-285">Этот URI содержит имя виртуального жесткого диска hello базового образа и его учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="02e7e-285">This URI contains hello base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="02e7e-286">Второй этап: подготовка новых виртуальных машин в Azure</span><span class="sxs-lookup"><span data-stu-id="02e7e-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="02e7e-287">Подготовка новых виртуальных машин на основе с AzureRMVMConfig создать с помощью hello базовый образ виртуального жесткого диска, записанный в первый этап, с помощью AcceleratedNetworking включена hello виртуального сетевого адаптера:</span><span class="sxs-lookup"><span data-stu-id="02e7e-287">Provision new VMs based with New-AzureRMVMConfig using hello base image VHD captured in phase one, with AcceleratedNetworking enabled on hello vNIC:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="02e7e-288">После загрузки виртуальных машин, проверьте устройство VF hello, «lspci» и проверьте запись Mellanox hello.</span><span class="sxs-lookup"><span data-stu-id="02e7e-288">After VMs boot up, check hello VF device by "lspci" and check hello Mellanox entry.</span></span> <span data-ttu-id="02e7e-289">Например мы должны увидеть этот элемент в выходных данных lspci hello:</span><span class="sxs-lookup"><span data-stu-id="02e7e-289">For example, we should see this item in hello lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="02e7e-290">Выполните сценарии hello резервирование с помощью:</span><span class="sxs-lookup"><span data-stu-id="02e7e-290">Run hello bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="02e7e-291">Перезагрузите hello новые виртуальные машины:</span><span class="sxs-lookup"><span data-stu-id="02e7e-291">Reboot hello new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="02e7e-292">Hello виртуальной Машины должен начинаться с bond0 настроен и hello Accelerated сетевые пути включена.</span><span class="sxs-lookup"><span data-stu-id="02e7e-292">hello VM should start with bond0 configured and hello Accelerated Networking path enabled.</span></span>  <span data-ttu-id="02e7e-293">Запустите `ifconfig` tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="02e7e-293">Run `ifconfig` tooconfirm.</span></span>
