---
title: "aaaNetwork сопоставление двух регионов Azure в Azure Site Recovery | Документы Microsoft"
description: "Azure Site Recovery координирует hello репликации, отработки отказа и восстановления виртуальных машин и физических серверов. Дополнительные сведения о tooAzure отработки отказа или вторичный центр обработки данных."
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
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="c82eb-104">Сетевое сопоставление между двумя регионами Azure</span><span class="sxs-lookup"><span data-stu-id="c82eb-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="c82eb-105">В этой статье описывается как toomap Azure виртуальные сети двух регионов Azure друг с другом.</span><span class="sxs-lookup"><span data-stu-id="c82eb-105">This article describes how toomap Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="c82eb-106">Сетевое сопоставление гарантирует, что при создании реплицированной виртуальной машины в целевом hello регион Azure, создается hello виртуальной сети, сопоставленные toovirtual сети hello исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c82eb-106">Network mapping ensures that when replicated virtual machine is created in hello target Azure region, it is created on hello virtual network that is mapped toovirtual network of hello source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="c82eb-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c82eb-107">Prerequisites</span></span>
<span data-ttu-id="c82eb-108">Перед сопоставлением сетей убедитесь, что в исходном и целевом регионе Azure созданы [виртуальные сети Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c82eb-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="c82eb-109">Сопоставление сетей</span><span class="sxs-lookup"><span data-stu-id="c82eb-109">Map networks</span></span>

<span data-ttu-id="c82eb-110">toomap виртуальной сети Azure в виртуальной сети tooanother одного региона Azure в другую область, последовательно выберите tooSite восстановления инфраструктуры -> Сетевое сопоставление (для виртуальных машин Azure) и создать сопоставление сети.</span><span class="sxs-lookup"><span data-stu-id="c82eb-110">toomap an Azure virtual network in one Azure region tooanother virtual network in another region, go tooSite Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="c82eb-112">В hello в приведенном ниже примере виртуальная машина работает в регионе Восточная Азия и выполняется реплицированные tooSoutheast Азии.</span><span class="sxs-lookup"><span data-stu-id="c82eb-112">In hello example below my virtual machine is running in East Asia region and is being replicated tooSoutheast Asia.</span></span>

<span data-ttu-id="c82eb-113">Выберите hello исходная и целевая сеть и нажмите кнопку ОК toocreate сетевое сопоставление из tooSoutheast Восточная Азия Азии.</span><span class="sxs-lookup"><span data-stu-id="c82eb-113">Select hello source and target network and then click OK toocreate a network mapping from East Asia tooSoutheast Asia.</span></span>

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="c82eb-115">Здравствуйте же самое toocreate сетевое сопоставление из tooEast Азии, Юго-Восточная Азия.</span><span class="sxs-lookup"><span data-stu-id="c82eb-115">Do hello same thing toocreate a network mapping from Southeast Asia tooEast Asia.</span></span>  
![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="c82eb-117">Сетевое сопоставление при включении репликации</span><span class="sxs-lookup"><span data-stu-id="c82eb-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="c82eb-118">Если сетевое сопоставление не выполняется, если выполняется репликация виртуальной машины для hello первый раз формы один регион Azure tooanother, затем можно выбрать целевую сеть как часть hello одного процесса.</span><span class="sxs-lookup"><span data-stu-id="c82eb-118">If network mapping is not done when you are replicating a virtual machine for hello first time form one Azure region tooanother, then you can choose target network as part of hello same process.</span></span> <span data-ttu-id="c82eb-119">Site Recovery создает сопоставления сетей из области tootarget области источника и целевой регион toosource области на основе выбора.</span><span class="sxs-lookup"><span data-stu-id="c82eb-119">Site Recovery creates network mappings from source region tootarget region and from target region toosource region based on this selection.</span></span>   

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="c82eb-121">По умолчанию Site Recovery создает сеть в целевой регион hello, идентичные toohello Исходная сеть и путем добавления "-asr" в качестве суффикса имени toohello hello исходную сеть.</span><span class="sxs-lookup"><span data-stu-id="c82eb-121">By default, Site Recovery creates a network in hello target region that is identical toohello source network and by adding '-asr' as a suffix toohello name of hello source network.</span></span> <span data-ttu-id="c82eb-122">Щелкните "Настройка", чтобы выбрать созданную ранее сеть.</span><span class="sxs-lookup"><span data-stu-id="c82eb-122">You can choose an already created network by clicking Customize.</span></span>

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="c82eb-124">Если hello сетевое сопоставление уже выполнено, нельзя изменить hello целевой виртуальной сети при включении репликации.</span><span class="sxs-lookup"><span data-stu-id="c82eb-124">If hello network mapping is already done, you can't change hello target virtual network while enabling replication.</span></span> <span data-ttu-id="c82eb-125">toochange, измените существующее сетевое сопоставление.</span><span class="sxs-lookup"><span data-stu-id="c82eb-125">toochange it, modify existing network mapping.</span></span>  

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Сетевое сопоставление](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="c82eb-128">При изменении сетевого сопоставления из области 1 tooregion-2, убедитесь, что вы измените сопоставление сети hello из области 2 tooregion-1 также.</span><span class="sxs-lookup"><span data-stu-id="c82eb-128">If you modify a network mapping from region-1 tooregion-2, make sure you modify hello network mapping from region-2 tooregion-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="c82eb-129">Выбор подсети</span><span class="sxs-lookup"><span data-stu-id="c82eb-129">Subnet selection</span></span>
<span data-ttu-id="c82eb-130">Подсеть виртуальной машины hello выбирается на основе имени hello подсети hello hello исходной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c82eb-130">Subnet of hello target virtual machine is selected based on hello name of hello subnet of hello source virtual machine.</span></span> <span data-ttu-id="c82eb-131">Если подсеть hello одинаковые имена, что и hello исходной виртуальной машины в целевой сети hello, затем, выбирать для hello целевой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c82eb-131">If there is a subnet of hello same name as that of hello source virtual machine available in hello target network, then that is chosen for hello target virtual machine.</span></span> <span data-ttu-id="c82eb-132">Если подсеть с hello одинаковые имена в целевой сети hello, а затем по алфавиту первая подсеть выбирается как hello целевой подсети.</span><span class="sxs-lookup"><span data-stu-id="c82eb-132">If there is no subnet with hello same name in hello target network, then alphabetically first subnet is chosen as hello target subnet.</span></span> <span data-ttu-id="c82eb-133">Подсети можно изменить, выбрав tooCompute, а также параметры сети виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="c82eb-133">You can modify this subnet by going tooCompute and Network settings of hello virtual machine.</span></span>

![Изменение подсети](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="c82eb-135">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="c82eb-135">IP address</span></span>

<span data-ttu-id="c82eb-136">IP-адрес для каждого сетевого интерфейса hello hello целевой виртуальной машины выбран следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c82eb-136">IP address for each of hello network interface of hello target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="c82eb-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="c82eb-137">DHCP</span></span>
<span data-ttu-id="c82eb-138">Если сетевой интерфейс hello hello исходной виртуальной машине с помощью DHCP, сетевому интерфейсу hello целевая виртуальная машина также задан как DHCP.</span><span class="sxs-lookup"><span data-stu-id="c82eb-138">If hello network interface of hello source virtual machine is using DHCP, then network interface of hello target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="c82eb-139">Статический IP-адрес</span><span class="sxs-lookup"><span data-stu-id="c82eb-139">Static IP</span></span>
<span data-ttu-id="c82eb-140">Если сетевой интерфейс hello hello исходной виртуальной машине использует статический IP-адрес, сетевой интерфейс виртуальной машины hello также устанавливается toouse статический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c82eb-140">If hello network interface of hello source virtual machine is using Static IP, then network interface of hello target virtual machine is also set toouse Static IP.</span></span> <span data-ttu-id="c82eb-141">Статический IP-адрес можно выбрать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c82eb-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="c82eb-142">Одинаковое пространство адресов</span><span class="sxs-lookup"><span data-stu-id="c82eb-142">Same address space</span></span>

<span data-ttu-id="c82eb-143">Если подсеть hello источника и целевой подсети hello имеют hello же адресное пространство, то целевой IP-адрес задается то же, что hello IP-адреса сетевого интерфейса hello hello исходной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c82eb-143">If hello source subnet and hello target subnet have hello same address space, then target IP is set same as hello IP of  hello network interface of hello source virtual machine.</span></span> <span data-ttu-id="c82eb-144">Если IP-адрес недоступен, некоторые другие доступный IP-адрес задан как hello целевой IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c82eb-144">If same IP is not available, then some other available IP is set as hello target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="c82eb-145">Разное пространство адресов</span><span class="sxs-lookup"><span data-stu-id="c82eb-145">Different address space</span></span>

<span data-ttu-id="c82eb-146">Если подсеть источника hello и hello целевой подсети имеют разные адресное пространство, целевой IP-адрес задан как любой доступный IP-адрес в hello целевой подсети.</span><span class="sxs-lookup"><span data-stu-id="c82eb-146">If hello source subnet and hello target subnet have different address space, then target IP is set as any available IP in hello target subnet.</span></span>

<span data-ttu-id="c82eb-147">Hello целевой IP-адрес каждого сетевого интерфейса можно изменить, выбрав tooCompute, а также параметры сети виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="c82eb-147">You can modify hello target IP on each network interface by going tooCompute and Network settings of hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c82eb-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c82eb-148">Next steps</span></span>

- <span data-ttu-id="c82eb-149">Дополнительные сведения о репликации виртуальных машин см. в [этой статье](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="c82eb-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
