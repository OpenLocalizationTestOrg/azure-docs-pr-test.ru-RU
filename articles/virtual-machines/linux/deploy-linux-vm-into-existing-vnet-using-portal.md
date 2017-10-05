---
title: "Развертывание виртуальных машин Linux в существующей сети с помощью портала Azure | Документация Майкрософт"
description: "Разверните виртуальную машину Linux в существующей виртуальной сети Azure с помощью портала."
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
ms.openlocfilehash: 964c0fc41773b50a9fbe476df47460484c2ada66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-portal"></a><span data-ttu-id="235cf-103">Как развернуть виртуальную машину Linux в существующей виртуальной сети Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="235cf-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure portal</span></span>

<span data-ttu-id="235cf-104">В этой статье показано, как развернуть виртуальную машину в существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="235cf-104">This article shows you how to deploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="235cf-105">Ресурсы Azure, такие как виртуальные сети и группы безопасности сети, должны быть статическими. Они должны долго храниться и редко развертываться.</span><span class="sxs-lookup"><span data-stu-id="235cf-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="235cf-106">После развертывания виртуальной сети ее можно повторно использовать при постоянных повторных развертываниях. Инфраструктура при этом не пострадает.</span><span class="sxs-lookup"><span data-stu-id="235cf-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="235cf-107">Воспринимайте виртуальную сеть как традиционный аппаратный сетевой коммутатор. Вам не понадобится настраивать новый аппаратный коммутатор при каждом развертывании.</span><span class="sxs-lookup"><span data-stu-id="235cf-107">Thinking about a VNet as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="235cf-108">Если виртуальная сеть правильно настроена, вы можете развертывать в ней новые серверы снова и снова, внося некоторые изменения во время ее использования (если они потребуются).</span><span class="sxs-lookup"><span data-stu-id="235cf-108">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="235cf-109">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="235cf-109">Create the resource group</span></span>

<span data-ttu-id="235cf-110">Сначала создайте группу ресурсов, чтобы упорядочить все компоненты, которые будут созданы в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="235cf-110">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="235cf-111">Дополнительные сведения о группах ресурсов Azure см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="235cf-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-the-vnet"></a><span data-ttu-id="235cf-113">Создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="235cf-113">Create the VNet</span></span>

<span data-ttu-id="235cf-114">Теперь создайте виртуальную сеть для запуска виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="235cf-114">Next, build a VNet to launch the VMs into.</span></span> <span data-ttu-id="235cf-115">Виртуальная сеть содержит одну подсеть. Она связывается с группой безопасности сети этой подсети на одном из следующих шагов.</span><span class="sxs-lookup"><span data-stu-id="235cf-115">The VNet contains one subnet and is associated with the network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="235cf-117">Добавление виртуальной сетевой карты в подсеть</span><span class="sxs-lookup"><span data-stu-id="235cf-117">Add a VNic to the subnet</span></span>

<span data-ttu-id="235cf-118">Виртуальные сетевые карты (VNic) имеют большое значение, так как они подключаются к разным виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="235cf-118">Virtual network cards (VNics) are important as you can connect them to different VMs.</span></span> <span data-ttu-id="235cf-119">Это позволяет использовать виртуальную сетевую карту как статический ресурс, тогда как виртуальные машины могут быть временными.</span><span class="sxs-lookup"><span data-stu-id="235cf-119">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="235cf-120">Создайте виртуальную сетевую карту и свяжите ее с подсетью, созданной на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="235cf-120">Create a VNic and associate it with the subnet created in the previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-the-network-security-group"></a><span data-ttu-id="235cf-122">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="235cf-122">Create the network security group</span></span>

<span data-ttu-id="235cf-123">На уровне сети группы безопасности сети Azure эквивалентны брандмауэру.</span><span class="sxs-lookup"><span data-stu-id="235cf-123">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="235cf-124">Дополнительные сведения о группах безопасности сети Azure см. в статье [Фильтрация сетевого трафика с помощью групп безопасности сети](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="235cf-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="235cf-126">Добавление правила, разрешающего входящий трафик по протоколу SSH</span><span class="sxs-lookup"><span data-stu-id="235cf-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="235cf-127">Виртуальной машине требуется доступ к Интернету, поэтому создается правило, разрешающее передачу входящего трафика в сети через порт 22 на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="235cf-127">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-the-nsg-with-the-subnet"></a><span data-ttu-id="235cf-129">Связывание группы безопасности сети с подсетью</span><span class="sxs-lookup"><span data-stu-id="235cf-129">Associate the NSG with the subnet</span></span>

<span data-ttu-id="235cf-130">Создав виртуальную сеть и подсеть, мы свяжем группу безопасности сети с подсетью.</span><span class="sxs-lookup"><span data-stu-id="235cf-130">With the VNet and the subnet created, associate the network security group with the subnet.</span></span> <span data-ttu-id="235cf-131">Группы безопасности сети можно связать со всей подсетью или с отдельной виртуальной сетевой картой.</span><span class="sxs-lookup"><span data-stu-id="235cf-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="235cf-132">Благодаря фильтрации трафика с помощью брандмауэра на уровне подсети все виртуальные сетевые карты и виртуальные машины в подсети защищаются с помощью группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="235cf-132">With the firewall filtering traffic at the subnet level, all VNics and the VMs within the subnet are protected by the network security group.</span></span> <span data-ttu-id="235cf-133">Также можно связать группу безопасности сети с одной виртуальной сетевой картой и защитить только одну виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="235cf-133">The other approach is the network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="235cf-135">Развертывание виртуальной машины в виртуальной сети и группе безопасности сети</span><span class="sxs-lookup"><span data-stu-id="235cf-135">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="235cf-136">С помощью Azure CLI можно развернуть виртуальную машину Linux в существующей группе ресурсов Azure, виртуальной сети, подсети и виртуальной сетевой карте.</span><span class="sxs-lookup"><span data-stu-id="235cf-136">Using the Azure portal, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="235cf-138">Используя портал для выбора существующих ресурсов, дайте среде Azure инструкцию развернуть виртуальную машину в существующей сети.</span><span class="sxs-lookup"><span data-stu-id="235cf-138">By using the portal to choose existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="235cf-139">После развертывания виртуальную сеть и подсеть можно оставить в качестве статических или постоянных ресурсов в регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="235cf-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="235cf-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="235cf-140">Next steps</span></span>

* [<span data-ttu-id="235cf-141">Развертывание виртуальных машин и управление ими с помощью шаблонов диспетчера ресурсов Azure и интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="235cf-141">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="235cf-142">Создание полной среды Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="235cf-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="235cf-143">Создание виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="235cf-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
