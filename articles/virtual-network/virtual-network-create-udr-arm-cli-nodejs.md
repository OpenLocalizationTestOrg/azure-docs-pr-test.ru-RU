---
title: "Здравствуйте, aaaControl маршрутизации и виртуальных устройств с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocontrol маршрутизации и виртуальных устройств с помощью hello Azure CLI 1.0."
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
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a><span data-ttu-id="6c806-103">Создайте маршруты определяемые пользователем (UDR) с помощью hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6c806-103">Create User-Defined Routes (UDR) using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c806-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c806-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="6c806-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="6c806-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="6c806-106">Шаблон</span><span class="sxs-lookup"><span data-stu-id="6c806-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="6c806-107">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="6c806-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="6c806-108">Интерфейс командной строки (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="6c806-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="6c806-109">Создание пользовательских маршрутизации и виртуальных устройств с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6c806-109">Create custom routing and virtual appliances using hello Azure CLI.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="6c806-110">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="6c806-110">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="6c806-111">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="6c806-111">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="6c806-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="6c806-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6c806-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="6c806-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="6c806-114">приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан на основании hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="6c806-114">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="6c806-115">Toorun hello команд, отображаемых в этом документе, сначала построения необходимо hello тестовой среды, развернув [этот шаблон](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello При необходимости и выполнения инструкции hello в hello портала.</span><span class="sxs-lookup"><span data-stu-id="6c806-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="6c806-116">Создать hello UDR для интерфейса подсети hello</span><span class="sxs-lookup"><span data-stu-id="6c806-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="6c806-117">Таблица маршрутов toocreate hello и маршрутов для подсети hello переднего плана, в зависимости от варианта hello выше, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="6c806-117">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="6c806-118">Выполните следующие команды toocreate hello таблицы маршрутов для подсети интерфейса hello:</span><span class="sxs-lookup"><span data-stu-id="6c806-118">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="6c806-119">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="6c806-119">Output:</span></span>
   
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
   
    <span data-ttu-id="6c806-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="6c806-120">Parameters:</span></span>
   
   * <span data-ttu-id="6c806-121">**-g (или --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="6c806-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="6c806-122">Имя группы ресурсов hello, где будут создаваться hello UDR.</span><span class="sxs-lookup"><span data-stu-id="6c806-122">Name of hello resource group where hello UDR will be created.</span></span> <span data-ttu-id="6c806-123">В данном сценарии это *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="6c806-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="6c806-124">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="6c806-124">**-l (or --location)**.</span></span> <span data-ttu-id="6c806-125">Регион Azure, где hello новый UDR будет создан.</span><span class="sxs-lookup"><span data-stu-id="6c806-125">Azure region where hello new UDR will be created.</span></span> <span data-ttu-id="6c806-126">В нашем случае это *westus*.</span><span class="sxs-lookup"><span data-stu-id="6c806-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="6c806-127">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="6c806-127">**-n (or --name)**.</span></span> <span data-ttu-id="6c806-128">Имя для hello новый UDR.</span><span class="sxs-lookup"><span data-stu-id="6c806-128">Name for hello new UDR.</span></span> <span data-ttu-id="6c806-129">В данном сценарии это *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="6c806-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="6c806-130">Запустите все toohello внутренней подсети (192.168.2.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="6c806-130">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="6c806-131">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="6c806-131">Output:</span></span>
   
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
   
    <span data-ttu-id="6c806-132">Параметры</span><span class="sxs-lookup"><span data-stu-id="6c806-132">Parameters:</span></span>
   
   * <span data-ttu-id="6c806-133">**-r (или --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="6c806-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="6c806-134">Имя таблицы маршрутов hello, куда будут добавлены hello маршрута.</span><span class="sxs-lookup"><span data-stu-id="6c806-134">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="6c806-135">В данном сценарии это *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="6c806-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="6c806-136">**-a (или --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="6c806-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="6c806-137">Префикс адреса для подсети hello, где пакеты, предназначенные для.</span><span class="sxs-lookup"><span data-stu-id="6c806-137">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="6c806-138">В данном сценарии это *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="6c806-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="6c806-139">**-y (или --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="6c806-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="6c806-140">Тип объекта, куда будет отправляться трафик.</span><span class="sxs-lookup"><span data-stu-id="6c806-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="6c806-141">Возможные значения: *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* или *None*.</span><span class="sxs-lookup"><span data-stu-id="6c806-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="6c806-142">**-p (или --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="6c806-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="6c806-143">IP-адрес следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="6c806-143">IP address for next hop.</span></span> <span data-ttu-id="6c806-144">В нашем случае это *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="6c806-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="6c806-145">Выполнения hello следующая команда созданную с hello таблицу маршрутов hello tooassociate **переднего плана** подсети:</span><span class="sxs-lookup"><span data-stu-id="6c806-145">Run hello following command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="6c806-146">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="6c806-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
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
   
    <span data-ttu-id="6c806-147">Параметры</span><span class="sxs-lookup"><span data-stu-id="6c806-147">Parameters:</span></span>
   
   * <span data-ttu-id="6c806-148">**-e (или --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="6c806-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="6c806-149">Имя виртуальной сети, где находится подсети hello hello.</span><span class="sxs-lookup"><span data-stu-id="6c806-149">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="6c806-150">В данном сценарии это *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="6c806-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="6c806-151">Создать hello UDR для hello внутренней подсети</span><span class="sxs-lookup"><span data-stu-id="6c806-151">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="6c806-152">toocreate hello таблицы маршрутов и маршрутизации для подсети hello серверной части, в зависимости от варианта hello выше завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="6c806-152">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="6c806-153">Выполните следующие команды toocreate hello таблицы маршрутов для подсети внутренней hello:</span><span class="sxs-lookup"><span data-stu-id="6c806-153">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="6c806-154">Запустите все toohello интерфейса подсети (192.168.1.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="6c806-154">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="6c806-155">Выполнения hello следующие таблицы маршрутов hello tooassociate команды с hello **серверной** подсети:</span><span class="sxs-lookup"><span data-stu-id="6c806-155">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="6c806-156">Включение IP-пересылки на FW1</span><span class="sxs-lookup"><span data-stu-id="6c806-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="6c806-157">tooenable IP-пересылки в hello сетевой Адаптер, используемый с **FW1**полный hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6c806-157">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="6c806-158">Выполните команду hello, которое следует и обратите внимание, значение hello **включить IP-пересылки**.</span><span class="sxs-lookup"><span data-stu-id="6c806-158">Run hello command that follows and notice hello value for **Enable IP forwarding**.</span></span> <span data-ttu-id="6c806-159">Оно должно быть задано слишком*false*.</span><span class="sxs-lookup"><span data-stu-id="6c806-159">It should be set too*false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="6c806-160">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="6c806-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
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
2. <span data-ttu-id="6c806-161">Выполните следующие команды tooenable IP-пересылки hello.</span><span class="sxs-lookup"><span data-stu-id="6c806-161">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="6c806-162">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="6c806-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
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
   
    <span data-ttu-id="6c806-163">Параметры</span><span class="sxs-lookup"><span data-stu-id="6c806-163">Parameters:</span></span>
   
   * <span data-ttu-id="6c806-164">**-f (или --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="6c806-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="6c806-165">Значение *true* или *false*.</span><span class="sxs-lookup"><span data-stu-id="6c806-165">*true* or *false*.</span></span>

