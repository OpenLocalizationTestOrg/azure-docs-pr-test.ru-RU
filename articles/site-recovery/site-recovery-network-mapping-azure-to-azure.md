---
title: "Сетевое сопоставление между двумя регионами Azure в Azure Site Recovery | Документация Майкрософт"
description: "Azure Site Recovery координирует репликацию, отработку отказа и восстановление виртуальных машин и физических серверов. Узнайте о функции отработки отказа с выполнением переноса в Azure или в дополнительный центр обработки данных."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 9d6a806ec533259797080fbfee2c38f918ebd8a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="aaa3f-104">Сетевое сопоставление между двумя регионами Azure</span><span class="sxs-lookup"><span data-stu-id="aaa3f-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="aaa3f-105">В этой статье описывается, как сопоставлять виртуальные сети Azure из двух регионов Azure друг с другом.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-105">This article describes how to map Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="aaa3f-106">Сетевое сопоставление гарантирует, что при создании реплицированной виртуальной машины в целевом регионе Azure, она создается в виртуальной сети, сопоставленной с виртуальной сетью исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-106">Network mapping ensures that when replicated virtual machine is created in the target Azure region, it is created on the virtual network that is mapped to virtual network of the source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="aaa3f-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="aaa3f-107">Prerequisites</span></span>
<span data-ttu-id="aaa3f-108">Перед сопоставлением сетей убедитесь, что в исходном и целевом регионе Azure созданы [виртуальные сети Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aaa3f-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="aaa3f-109">Сопоставление сетей</span><span class="sxs-lookup"><span data-stu-id="aaa3f-109">Map networks</span></span>

<span data-ttu-id="aaa3f-110">Чтобы сопоставить виртуальную сеть Azure в одном регионе Azure с виртуальной сетью в другом регионе, выберите " Site Recovery Infrastructure (Инфраструктура Site Recovery) > Сетевое сопоставление" (для виртуальных машин Azure) и создайте сетевое сопоставление.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-110">To map an Azure virtual network in one Azure region to another virtual network in another region, go to Site Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="aaa3f-112">В приведенном ниже примере виртуальная машина выполняется в Восточной Азии и реплицируется в Юго-Восточную Азию.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-112">In the example below my virtual machine is running in East Asia region and is being replicated to Southeast Asia.</span></span>

<span data-ttu-id="aaa3f-113">Выберите исходную и целевую сеть, а затем нажмите кнопку ОК, чтобы создать сетевое сопоставление из Восточной Азии в Юго-Восточную.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-113">Select the source and target network and then click OK to create a network mapping from East Asia to Southeast Asia.</span></span>

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="aaa3f-115">Выполните ту же процедуру, чтобы создать сетевое сопоставление из Юго-Восточной Азии в Восточную.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-115">Do the same thing to create a network mapping from Southeast Asia to East Asia.</span></span>  
![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="aaa3f-117">Сетевое сопоставление при включении репликации</span><span class="sxs-lookup"><span data-stu-id="aaa3f-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="aaa3f-118">Если сетевое сопоставление не выполняется при первой репликации виртуальной машины из одного региона Azure в другой, в рамках одного процесса можно выбрать целевую сеть.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-118">If network mapping is not done when you are replicating a virtual machine for the first time form one Azure region to another, then you can choose target network as part of the same process.</span></span> <span data-ttu-id="aaa3f-119">Site Recovery создает сетевое сопоставление из исходного региона в целевой и наоборот (в зависимости от вашего выбора).</span><span class="sxs-lookup"><span data-stu-id="aaa3f-119">Site Recovery creates network mappings from source region to target region and from target region to source region based on this selection.</span></span>   

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="aaa3f-121">По умолчанию Site Recovery создает сеть в целевом регионе, которая идентична исходной сети, и добавляет суффикс -asr к имени исходной сети.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-121">By default, Site Recovery creates a network in the target region that is identical to the source network and by adding '-asr' as a suffix to the name of the source network.</span></span> <span data-ttu-id="aaa3f-122">Щелкните "Настройка", чтобы выбрать созданную ранее сеть.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-122">You can choose an already created network by clicking Customize.</span></span>

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="aaa3f-124">Если сетевое сопоставление уже выполнено, изменить целевую виртуальную сеть при включении репликации нельзя.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-124">If the network mapping is already done, you can't change the target virtual network while enabling replication.</span></span> <span data-ttu-id="aaa3f-125">Чтобы ее изменить, измените имеющееся сетевое сопоставление.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-125">To change it, modify existing network mapping.</span></span>  

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="aaa3f-128">Если вы изменили сетевое сопоставление из региона 1 в регион 2, убедитесь, что сетевое сопоставление из региона 2 в регион 1 было также изменено.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-128">If you modify a network mapping from region-1 to region-2, make sure you modify the network mapping from region-2 to region-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="aaa3f-129">Выбор подсети</span><span class="sxs-lookup"><span data-stu-id="aaa3f-129">Subnet selection</span></span>
<span data-ttu-id="aaa3f-130">Подсеть целевой виртуальной машины выбирается на основе имени подсети исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-130">Subnet of the target virtual machine is selected based on the name of the subnet of the source virtual machine.</span></span> <span data-ttu-id="aaa3f-131">Если подсеть имеет одинаковое имя с исходной виртуальной машиной в целевой сети, она будет выбрана для целевой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-131">If there is a subnet of the same name as that of the source virtual machine available in the target network, then that is chosen for the target virtual machine.</span></span> <span data-ttu-id="aaa3f-132">Когда в целевой сети нет подсети с тем же именем, в качестве целевой подсети будет выбрана первая подсеть в алфавитном порядке.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-132">If there is no subnet with the same name in the target network, then alphabetically first subnet is chosen as the target subnet.</span></span> <span data-ttu-id="aaa3f-133">Чтобы изменить подсеть, выберите параметры вычислений и сети виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-133">You can modify this subnet by going to Compute and Network settings of the virtual machine.</span></span>

![Изменение подсети](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="aaa3f-135">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="aaa3f-135">IP address</span></span>

<span data-ttu-id="aaa3f-136">IP-адрес для каждого сетевого интерфейса целевой виртуальной машины можно выбрать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="aaa3f-136">IP address for each of the network interface of the target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="aaa3f-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="aaa3f-137">DHCP</span></span>
<span data-ttu-id="aaa3f-138">Если сетевой интерфейс исходной виртуальной машины использует DHCP, то сетевому интерфейсу целевой виртуальной машины будет также задан DHCP.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-138">If the network interface of the source virtual machine is using DHCP, then network interface of the target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="aaa3f-139">Статический IP-адрес</span><span class="sxs-lookup"><span data-stu-id="aaa3f-139">Static IP</span></span>
<span data-ttu-id="aaa3f-140">Если сетевой интерфейс исходной виртуальной машины использует статический IP-адрес, то сетевой интерфейс целевой виртуальной машины будет также его использовать.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-140">If the network interface of the source virtual machine is using Static IP, then network interface of the target virtual machine is also set to use Static IP.</span></span> <span data-ttu-id="aaa3f-141">Статический IP-адрес можно выбрать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="aaa3f-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="aaa3f-142">Одинаковое пространство адресов</span><span class="sxs-lookup"><span data-stu-id="aaa3f-142">Same address space</span></span>

<span data-ttu-id="aaa3f-143">Если исходная и целевая подсети имеют одинаковое пространство адресов, будет использоваться тот же целевой IP-адрес, что и в сетевом интерфейсе исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-143">If the source subnet and the target subnet have the same address space, then target IP is set same as the IP of  the network interface of the source virtual machine.</span></span> <span data-ttu-id="aaa3f-144">Если тот же IP-адрес недоступен, в качестве целевого IP-адреса будет задан другой доступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-144">If same IP is not available, then some other available IP is set as the target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="aaa3f-145">Разное пространство адресов</span><span class="sxs-lookup"><span data-stu-id="aaa3f-145">Different address space</span></span>

<span data-ttu-id="aaa3f-146">Если исходная и целевая подсети имеют разное пространство адресов, будет задан любой из доступных IP-адресов в целевой подсети.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-146">If the source subnet and the target subnet have different address space, then target IP is set as any available IP in the target subnet.</span></span>

<span data-ttu-id="aaa3f-147">Чтобы изменить целевой IP-адрес каждого сетевого интерфейса, выберите параметры вычислений и сети виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aaa3f-147">You can modify the target IP on each network interface by going to Compute and Network settings of the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaa3f-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aaa3f-148">Next steps</span></span>

- <span data-ttu-id="aaa3f-149">Дополнительные сведения о репликации виртуальных машин см. в [этой статье](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="aaa3f-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
