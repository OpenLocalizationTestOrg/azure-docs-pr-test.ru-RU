---
title: "Управление маршрутизацией и виртуальными модулями с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Сведения о том, как управлять маршрутизацией и виртуальными модулями с помощью Azure CLI 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 5f21bc7a4fcd9507ea9d6b2b752a2328a7b834f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-10"></a><span data-ttu-id="64ad9-103">Создание определяемых пользователем маршрутов с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="64ad9-103">Create User-Defined Routes (UDR) using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="64ad9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="64ad9-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="64ad9-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="64ad9-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="64ad9-106">Шаблон</span><span class="sxs-lookup"><span data-stu-id="64ad9-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="64ad9-107">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="64ad9-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="64ad9-108">Интерфейс командной строки (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="64ad9-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="64ad9-109">Создание настраиваемой маршрутизации и виртуальных модулей с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="64ad9-109">Create custom routing and virtual appliances using the Azure CLI.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="64ad9-110">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="64ad9-110">CLI versions to complete the task</span></span> 

<span data-ttu-id="64ad9-111">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="64ad9-111">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="64ad9-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="64ad9-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="64ad9-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="64ad9-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="64ad9-114">Для приведенных ниже примеров команд интерфейса командной строки Azure требуется уже созданная простая среда, основанная на приведенном выше сценарии.</span><span class="sxs-lookup"><span data-stu-id="64ad9-114">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="64ad9-115">Чтобы выполнять команды в том виде, в котором они представлены в этом документе, сначала создайте тестовую среду, развернув [этот шаблон](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), нажмите **Deploy to Azure**(Развернуть в Azure), при необходимости замените значения параметров по умолчанию и следуйте указаниям на портале.</span><span class="sxs-lookup"><span data-stu-id="64ad9-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="64ad9-116">Создание определяемого пользователем маршрута для интерфейсной подсети</span><span class="sxs-lookup"><span data-stu-id="64ad9-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="64ad9-117">Чтобы создать таблицу маршрутов и маршрут, необходимые для подсети переднего плана, на основании приведенного выше сценария, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="64ad9-117">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="64ad9-118">Чтобы создать таблицу маршрутов для интерфейсной подсети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="64ad9-118">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="64ad9-119">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="64ad9-119">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    <span data-ttu-id="64ad9-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="64ad9-120">Parameters:</span></span>
   
   * <span data-ttu-id="64ad9-121">**-g (или --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="64ad9-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="64ad9-122">Имя группы ресурсов, в которой будет создан определяемый пользователем маршрут.</span><span class="sxs-lookup"><span data-stu-id="64ad9-122">Name of the resource group where the UDR will be created.</span></span> <span data-ttu-id="64ad9-123">В данном сценарии это *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="64ad9-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="64ad9-124">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="64ad9-124">**-l (or --location)**.</span></span> <span data-ttu-id="64ad9-125">Регион Azure, в котором будет создан новый определяемый пользователем маршрут.</span><span class="sxs-lookup"><span data-stu-id="64ad9-125">Azure region where the new UDR will be created.</span></span> <span data-ttu-id="64ad9-126">В нашем случае это *westus*.</span><span class="sxs-lookup"><span data-stu-id="64ad9-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="64ad9-127">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="64ad9-127">**-n (or --name)**.</span></span> <span data-ttu-id="64ad9-128">Имя нового определяемого пользователем маршрута.</span><span class="sxs-lookup"><span data-stu-id="64ad9-128">Name for the new UDR.</span></span> <span data-ttu-id="64ad9-129">В данном сценарии это *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="64ad9-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="64ad9-130">Чтобы создать маршрут в таблице маршрутов для отправки всего трафика, предназначенного для серверной подсети (192.168.2.0/24), в виртуальную машину **FW1** (192.168.0.4), выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="64ad9-130">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="64ad9-131">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="64ad9-131">Output:</span></span>
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    <span data-ttu-id="64ad9-132">Параметры</span><span class="sxs-lookup"><span data-stu-id="64ad9-132">Parameters:</span></span>
   
   * <span data-ttu-id="64ad9-133">**-r (или --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="64ad9-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="64ad9-134">Имя таблицы маршрутов, куда будет добавлен маршрут.</span><span class="sxs-lookup"><span data-stu-id="64ad9-134">Name of the route table where the route will be added.</span></span> <span data-ttu-id="64ad9-135">В данном сценарии это *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="64ad9-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="64ad9-136">**-a (или --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="64ad9-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="64ad9-137">Префикс адреса для подсети, в которую адресованы пакеты.</span><span class="sxs-lookup"><span data-stu-id="64ad9-137">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="64ad9-138">В данном сценарии это *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="64ad9-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="64ad9-139">**-y (или --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="64ad9-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="64ad9-140">Тип объекта, куда будет отправляться трафик.</span><span class="sxs-lookup"><span data-stu-id="64ad9-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="64ad9-141">Возможные значения: *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* или *None*.</span><span class="sxs-lookup"><span data-stu-id="64ad9-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="64ad9-142">**-p (или --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="64ad9-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="64ad9-143">IP-адрес следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="64ad9-143">IP address for next hop.</span></span> <span data-ttu-id="64ad9-144">В нашем случае это *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="64ad9-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="64ad9-145">Чтобы сопоставить созданную выше таблицу маршрутов с подсетью **FrontEnd**, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="64ad9-145">Run the following command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="64ad9-146">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="64ad9-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    <span data-ttu-id="64ad9-147">Параметры</span><span class="sxs-lookup"><span data-stu-id="64ad9-147">Parameters:</span></span>
   
   * <span data-ttu-id="64ad9-148">**-e (или --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="64ad9-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="64ad9-149">Имя виртуальной сети, в которой расположена подсеть.</span><span class="sxs-lookup"><span data-stu-id="64ad9-149">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="64ad9-150">В данном сценарии это *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="64ad9-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="64ad9-151">Создание определяемого пользователем маршрута для серверной подсети</span><span class="sxs-lookup"><span data-stu-id="64ad9-151">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="64ad9-152">Чтобы создать таблицу маршрутов и маршрут, необходимые для серверной подсети, на основании приведенного выше сценария, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="64ad9-152">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="64ad9-153">Чтобы создать таблицу маршрутов для серверной подсети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="64ad9-153">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="64ad9-154">Чтобы создать маршрут в таблице маршрутов для отправки всего трафика, предназначенного для интерфейсной подсети (192.168.1.0/24), в виртуальную машину **FW1** (192.168.0.4), выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="64ad9-154">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="64ad9-155">Чтобы сопоставить таблицу маршрутов с подсетью **BackEnd**, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="64ad9-155">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="64ad9-156">Включение IP-пересылки на FW1</span><span class="sxs-lookup"><span data-stu-id="64ad9-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="64ad9-157">Чтобы включить IP-пересылку в сетевом интерфейсе, используемом **FW1**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="64ad9-157">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="64ad9-158">Выполните следующую команду и проверьте значение параметра **Enable IP forwarding** (Включить IP-пересылку).</span><span class="sxs-lookup"><span data-stu-id="64ad9-158">Run the command that follows and notice the value for **Enable IP forwarding**.</span></span> <span data-ttu-id="64ad9-159">Оно должно быть равно *false*.</span><span class="sxs-lookup"><span data-stu-id="64ad9-159">It should be set to *false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="64ad9-160">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="64ad9-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up the network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. <span data-ttu-id="64ad9-161">Чтобы включить IP-пересылку, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="64ad9-161">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="64ad9-162">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="64ad9-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up the network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up the network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    <span data-ttu-id="64ad9-163">Параметры</span><span class="sxs-lookup"><span data-stu-id="64ad9-163">Parameters:</span></span>
   
   * <span data-ttu-id="64ad9-164">**-f (или --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="64ad9-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="64ad9-165">Значение *true* или *false*.</span><span class="sxs-lookup"><span data-stu-id="64ad9-165">*true* or *false*.</span></span>

