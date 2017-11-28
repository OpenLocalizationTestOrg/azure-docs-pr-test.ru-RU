---
title: "aaaDeploy виртуальных машин Linux в существующей сети с портала Azure | Документы Microsoft"
description: "Развертывание виртуальной Машины Linux в существующей виртуальной сети Azure с помощью портала hello."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a><span data-ttu-id="61b48-103">Как toodeploy виртуальной машины Linux в существующей виртуальной сети Azure с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="61b48-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure portal</span></span>

<span data-ttu-id="61b48-104">В этой статье показано, как toodeploy виртуальной машины (VM) в существующей виртуальной сети (VNet).</span><span class="sxs-lookup"><span data-stu-id="61b48-104">This article shows you how toodeploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="61b48-105">Ресурсы Azure, такие как виртуальные сети и группы безопасности сети, должны быть статическими. Они должны долго храниться и редко развертываться.</span><span class="sxs-lookup"><span data-stu-id="61b48-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="61b48-106">После развертывания виртуальной сети, он может быть использован с константой повторные без инфраструктуры toohello любой негативно влияет на.</span><span class="sxs-lookup"><span data-stu-id="61b48-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="61b48-107">Размышления о виртуальной сети как обычный параметр сетевого оборудования — не потребуются tooconfigure нового оборудования переключиться с каждым развертыванием.</span><span class="sxs-lookup"><span data-stu-id="61b48-107">Thinking about a VNet as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="61b48-108">С правильно настроенной виртуальной сети можно будет продолжить toodeploy новых серверов в этой виртуальной сети и снова несколько, если таковые имеются, изменения, необходимые протяжении hello hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b48-108">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="61b48-109">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="61b48-109">Create hello resource group</span></span>

<span data-ttu-id="61b48-110">Сначала необходимо создаете группы ресурсов tooorganize все данные, создаваемые в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="61b48-110">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="61b48-111">Дополнительные сведения о группах ресурсов Azure см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61b48-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a><span data-ttu-id="61b48-113">Создать hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="61b48-113">Create hello VNet</span></span>

<span data-ttu-id="61b48-114">Затем выполнить сборку виртуальных машин в виртуальной сети toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="61b48-114">Next, build a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="61b48-115">Hello виртуальная сеть содержит одну подсеть и связан с hello сетевой группы безопасности с этой подсетью на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="61b48-115">hello VNet contains one subnet and is associated with hello network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="61b48-117">Добавить подсеть toohello виртуального сетевого адаптера</span><span class="sxs-lookup"><span data-stu-id="61b48-117">Add a VNic toohello subnet</span></span>

<span data-ttu-id="61b48-118">Виртуальные сетевые адаптеры (VNics) являются важной, так как их можно соединить toodifferent виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="61b48-118">Virtual network cards (VNics) are important as you can connect them toodifferent VMs.</span></span> <span data-ttu-id="61b48-119">Этот подход позволяет hello виртуального сетевого адаптера как статический ресурс, пока hello виртуальные машины могут быть как временными.</span><span class="sxs-lookup"><span data-stu-id="61b48-119">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="61b48-120">Создание виртуального сетевого адаптера и связать его с подсетью hello на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="61b48-120">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a><span data-ttu-id="61b48-122">Создание группы безопасности сети hello</span><span class="sxs-lookup"><span data-stu-id="61b48-122">Create hello network security group</span></span>

<span data-ttu-id="61b48-123">Эквивалентный tooa брандмауэра на уровне сети hello являются группы безопасности сети Azure.</span><span class="sxs-lookup"><span data-stu-id="61b48-123">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="61b48-124">Дополнительные сведения о группах безопасности сети Azure см. в статье [Фильтрация сетевого трафика с помощью групп безопасности сети](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="61b48-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="61b48-126">Добавление правила, разрешающего входящий трафик по протоколу SSH</span><span class="sxs-lookup"><span data-stu-id="61b48-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="61b48-127">Hello виртуальной Машины требуется доступ из hello Интернета, поэтому правило, разрешающее трафик toobe входящий порт 22 передаются через tooport сети hello 22 hello создается виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="61b48-127">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a><span data-ttu-id="61b48-129">Связать hello NSG с подсетью hello</span><span class="sxs-lookup"><span data-stu-id="61b48-129">Associate hello NSG with hello subnet</span></span>

<span data-ttu-id="61b48-130">Hello виртуальной сети и подсети hello создать свяжите hello сетевой группы безопасности с hello подсети.</span><span class="sxs-lookup"><span data-stu-id="61b48-130">With hello VNet and hello subnet created, associate hello network security group with hello subnet.</span></span> <span data-ttu-id="61b48-131">Группы безопасности сети можно связать со всей подсетью или с отдельной виртуальной сетевой картой.</span><span class="sxs-lookup"><span data-stu-id="61b48-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="61b48-132">С помощью брандмауэра hello фильтрации трафика на уровне подсети hello все VNics и hello виртуальные машины в подсети hello защищаются с помощью группы безопасности сети hello.</span><span class="sxs-lookup"><span data-stu-id="61b48-132">With hello firewall filtering traffic at hello subnet level, all VNics and hello VMs within hello subnet are protected by hello network security group.</span></span> <span data-ttu-id="61b48-133">Hello другого подхода является hello, группы безопасности сети связан только один виртуальный сетевой адаптер и защиту только одна виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="61b48-133">hello other approach is hello network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="61b48-135">Развертывание hello виртуальной Машины в виртуальной сети hello и NSG</span><span class="sxs-lookup"><span data-stu-id="61b48-135">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="61b48-136">Использование hello портал Azure, hello виртуальных Машин Linux — развернутой toohello существующие группы ресурсов Azure, виртуальной сети, подсети и виртуального сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="61b48-136">Using hello Azure portal, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="61b48-138">С помощью существующих ресурсов портала toochoose hello, вы указываете hello Azure toodeploy виртуальных Машин в существующей сети hello.</span><span class="sxs-lookup"><span data-stu-id="61b48-138">By using hello portal toochoose existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="61b48-139">После развертывания виртуальную сеть и подсеть можно оставить в качестве статических или постоянных ресурсов в регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="61b48-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="61b48-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61b48-140">Next steps</span></span>

* [<span data-ttu-id="61b48-141">Использовать toocreate шаблона диспетчера ресурсов Azure конкретного развертывания</span><span class="sxs-lookup"><span data-stu-id="61b48-141">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="61b48-142">Создание полной среды Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="61b48-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="61b48-143">Создание виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="61b48-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
