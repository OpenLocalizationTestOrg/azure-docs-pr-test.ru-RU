---
title: "Создание виртуальной сети с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Узнайте, как создать виртуальную сеть с помощью Azure CLI 1.0 в модели Resource Manager."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f0649c5c8c04dda72d2f147601efb37217f9bade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli"></a><span data-ttu-id="00356-103">Создание виртуальной сети с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="00356-103">Create a virtual network using the Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="00356-104">Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую.</span><span class="sxs-lookup"><span data-stu-id="00356-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="00356-105">Для создания ресурсов корпорация Майкрософт рекомендует использовать модель развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="00356-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="00356-106">Дополнительные сведения о различиях между двумя моделями см. в статье [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md) (Azure Resource Manager и классическое развертывание. Общие сведения о моделях развертывания и состоянии ресурсов).</span><span class="sxs-lookup"><span data-stu-id="00356-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="00356-107">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="00356-107">CLI versions to complete the task</span></span>
<span data-ttu-id="00356-108">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="00356-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="00356-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) — это интерфейс командной строки нового поколения для модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="00356-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span>
- <span data-ttu-id="00356-110">[Azure CLI 1.0](#create-a-virtual-network) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="00356-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for the classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="00356-111">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="00356-111">Create a virtual network</span></span>

<span data-ttu-id="00356-112">Чтобы создать виртуальную сеть с помощью интерфейса командной строки Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="00356-112">To create a virtual network using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="00356-113">Установите и настройте интерфейс командной строки Azure, следуя инструкциям в [этой статье](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="00356-113">Install and configure the Azure CLI by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="00356-114">Создайте виртуальную сеть и подсеть.</span><span class="sxs-lookup"><span data-stu-id="00356-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="00356-115">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="00356-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="00356-116">Используемые параметры:</span><span class="sxs-lookup"><span data-stu-id="00356-116">Parameters used:</span></span>

   * <span data-ttu-id="00356-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="00356-117">**--vnet**.</span></span> <span data-ttu-id="00356-118">Имя виртуальной сети, которую нужно будет создать.</span><span class="sxs-lookup"><span data-stu-id="00356-118">Name of the VNet to be created.</span></span> <span data-ttu-id="00356-119">В данном сценарии это *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="00356-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="00356-120">**-e (или --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="00356-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="00356-121">Адресное пространство виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="00356-121">VNet address space.</span></span> <span data-ttu-id="00356-122">В данном сценарии это *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="00356-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="00356-123">**-i (или -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="00356-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="00356-124">Маска подсети в формате CIDR.</span><span class="sxs-lookup"><span data-stu-id="00356-124">Network mask in CIDR format.</span></span> <span data-ttu-id="00356-125">В данном сценарии это *16*.</span><span class="sxs-lookup"><span data-stu-id="00356-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="00356-126">**-n (или --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="00356-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="00356-127">Имя первой подсети.</span><span class="sxs-lookup"><span data-stu-id="00356-127">Name of the first subnet.</span></span> <span data-ttu-id="00356-128">В данном сценарии это *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="00356-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="00356-129">**-p (или --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="00356-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="00356-130">Начальный IP-адрес для подсети или адресное пространство подсети.</span><span class="sxs-lookup"><span data-stu-id="00356-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="00356-131">В нашем сценарии это *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="00356-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="00356-132">**-r (или --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="00356-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="00356-133">Маска подсети в формате CIDR для подсети.</span><span class="sxs-lookup"><span data-stu-id="00356-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="00356-134">В данном сценарии это *24*.</span><span class="sxs-lookup"><span data-stu-id="00356-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="00356-135">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="00356-135">**-l (or --location)**.</span></span> <span data-ttu-id="00356-136">Регион Azure, в котором создается виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="00356-136">Azure region where the VNet is created.</span></span> <span data-ttu-id="00356-137">В данном сценарии это *Central US*.</span><span class="sxs-lookup"><span data-stu-id="00356-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="00356-138">Создайте подсеть.</span><span class="sxs-lookup"><span data-stu-id="00356-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="00356-139">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="00356-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="00356-140">Используемые параметры:</span><span class="sxs-lookup"><span data-stu-id="00356-140">Parameters used:</span></span>

   * <span data-ttu-id="00356-141">**-t (или --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="00356-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="00356-142">Имя виртуальной сети, в которой будет создана подсеть.</span><span class="sxs-lookup"><span data-stu-id="00356-142">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="00356-143">В данном сценарии это *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="00356-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="00356-144">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="00356-144">**-n (or --name)**.</span></span> <span data-ttu-id="00356-145">Имя новой подсети.</span><span class="sxs-lookup"><span data-stu-id="00356-145">Name of the new subnet.</span></span> <span data-ttu-id="00356-146">В нашем сценарии это *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="00356-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="00356-147">**-a (или --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="00356-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="00356-148">Блок подсети CIDR.</span><span class="sxs-lookup"><span data-stu-id="00356-148">Subnet CIDR block.</span></span> <span data-ttu-id="00356-149">В данном сценарии это *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="00356-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="00356-150">Вот как можно просмотреть свойства новой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="00356-150">To view the properties of the new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="00356-151">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="00356-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a><span data-ttu-id="00356-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="00356-152">Next steps</span></span>

<span data-ttu-id="00356-153">Инструкции по подключению:</span><span class="sxs-lookup"><span data-stu-id="00356-153">Learn how to connect:</span></span>

- <span data-ttu-id="00356-154">Сведения о подключении виртуальной машины к виртуальной сети см. в статье о [создании виртуальной машины Linux](../virtual-machines/linux/quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="00356-154">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="00356-155">Вместо создания виртуальной сети и подсети с помощью действий, описанных в этой статье, виртуальную машину можно подключить к имеющейся виртуальной сети и подсети.</span><span class="sxs-lookup"><span data-stu-id="00356-155">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="00356-156">Сведения об установке подключения между виртуальными сетями см. в статье [Настройка подключения между виртуальными сетями на портале Azure](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="00356-156">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="00356-157">Сведения о подключении виртуальной сети к локальной сети с использованием виртуальной частной сети типа "сеть — сеть" или канала ExpressRoute см. в</span><span class="sxs-lookup"><span data-stu-id="00356-157">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="00356-158">статьях [Добавление подключения типа "сеть — сеть" к виртуальной сети с помощью существующего подключения VPN-шлюза](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) и [Подключение виртуальной сети к каналу ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="00356-158">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>