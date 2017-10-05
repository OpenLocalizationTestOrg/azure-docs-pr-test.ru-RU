---
title: "Создание доступной в Интернете подсистемы балансировки нагрузки с помощью Azure CLI | Документация Майкрософт"
description: "Узнайте, как создать балансировщик нагрузки для Интернета в диспетчере ресурсов с помощью интерфейса командной строки Azure."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3b1780033cbc8aa3e108a213a4d2bfd0332fd7d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-load-balancer-using-the-azure-cli"></a><span data-ttu-id="8dc4e-103">Создание балансировщика нагрузки для Интернета с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8dc4e-103">Creating an internet load balancer using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8dc4e-104">Портал</span><span class="sxs-lookup"><span data-stu-id="8dc4e-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="8dc4e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8dc4e-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="8dc4e-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8dc4e-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="8dc4e-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="8dc4e-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="8dc4e-108">В этой статье описывается модель развертывания с использованием менеджера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="8dc4e-109">Вы также можете [узнать, как создать балансировщик нагрузки для Интернета, используя классическое развертывание](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8dc4e-109">You can also [Learn how to create an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="8dc4e-110">Развертывание решения с помощью интерфейса командной строки Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="8dc4e-110">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="8dc4e-111">Ниже описана процедура создания балансировщика нагрузки для Интернета с помощью Azure Resource Manager и интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-111">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="8dc4e-112">Azure Resource Manager позволяет по отдельности создавать и настраивать ресурсы, после чего на их основе создается единый ресурс.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-112">With Azure Resource Manager each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="8dc4e-113">Чтобы развернуть балансировщик нагрузки, необходимо создать и настроить следующие объекты.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="8dc4e-114">Конфигурация интерфейсных IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="8dc4e-115">Пул внутренних адресов. Содержит сетевые интерфейсы (сетевые карты) для получения виртуальными машинами трафика от балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-115">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="8dc4e-116">Правила балансировки нагрузки. Содержат правила сопоставления общего порта в балансировщике нагрузки с портом в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-116">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="8dc4e-117">Правила NAT для входящего трафика. Содержат правила сопоставления общего порта в балансировщике нагрузки с портом на конкретной виртуальной машине в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-117">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="8dc4e-118">Пробы. Содержат пробы работоспособности, с помощью которых можно проверить доступность экземпляров виртуальных машин в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-118">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="8dc4e-119">Дополнительные сведения см. в статье о [поддержке Azure Resource Manage для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8dc4e-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="8dc4e-120">Настройка интерфейса командной строки для использования Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8dc4e-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="8dc4e-121">Если вы еще не пользовались Azure CLI, ознакомьтесь со статьей [Установка и настройка CLI Azure](../cli-install-nodejs.md) и следуйте инструкциям вплоть до выбора учетной записи Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="8dc4e-122">Выполните команду **azure config mode** , чтобы переключиться в режим диспетчера ресурсов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="8dc4e-123">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8dc4e-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="8dc4e-124">Создание виртуальной сети и общедоступного IP-адреса для пула IP-адресов клиентской части</span><span class="sxs-lookup"><span data-stu-id="8dc4e-124">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="8dc4e-125">Создайте виртуальную сеть *NRPVnet* в регионе "Восток США" с помощью группы ресурсов *NRPRG*.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-125">Create a virtual network (VNet) named *NRPVnet* in the East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="8dc4e-126">Создайте подсеть *NRPVnetSubnet* с блоком CIDR 10.0.0.0/24 в виртуальной сети *NRPVnet*.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="8dc4e-127">Создайте общедоступный IP-адрес *NRPPublicIP*, который будет использоваться пулом интерфейсных IP-адресов, с DNS-именем *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-127">Create a public IP address named *NRPPublicIP* to be used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span> <span data-ttu-id="8dc4e-128">В команде ниже используется статическое выделение и время ожидания при простое 4 минуты.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-128">The command below uses the static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="8dc4e-129">Балансировщик нагрузки будет использовать метку домена общедоступного IP-адреса в качестве своего полного доменного имени (FQDN).</span><span class="sxs-lookup"><span data-stu-id="8dc4e-129">The load balancer will use the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="8dc4e-130">В этом заключается отличие от классического развертывания, при котором в качестве полного доменного имени балансировщика нагрузки используется облачная служба.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-130">This a change from classic deployment, which uses the cloud service as the load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="8dc4e-131">В этом примере используется полное доменное имя *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-131">In this example, the FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="8dc4e-132">Создание балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="8dc4e-132">Create a load balancer</span></span>

<span data-ttu-id="8dc4e-133">Приведенная ниже команда создает балансировщик нагрузки *NRPlb* в группе ресурсов *NRPRG*, размещенной в регионе Azure *Восточная часть США*.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-133">The following command creates a load balancer named *NRPlb* in the *NRPRG* resource group in the *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="8dc4e-134">Создание пула интерфейсных IP-адресов и пула внутренних адресов</span><span class="sxs-lookup"><span data-stu-id="8dc4e-134">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="8dc4e-135">В этом примере показано, как создать пул интерфейсных IP-адресов, который будет принимать входящий сетевой трафик для балансировщика нагрузки, а также пул внутренних IP-адресов, который будет отправлять сетевой трафик с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-135">This example demonstrates how to create the front-end IP pool that receives the incoming network traffic on the load balancer and the backend IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="8dc4e-136">Создайте пул интерфейсных IP-адресов, связывающий общедоступный IP-адрес, созданный на предыдущем этапе, и балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-136">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="8dc4e-137">Настройте пул внутренних адресов для приема входящего трафика из пула интерфейсных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-137">Set up a back-end address pool used to receive incoming traffic from the front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="8dc4e-138">Создание правил балансировки нагрузки, правил NAT и пробы</span><span class="sxs-lookup"><span data-stu-id="8dc4e-138">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="8dc4e-139">В этом примере создаются следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="8dc4e-139">This example creates the following items.</span></span>

* <span data-ttu-id="8dc4e-140">правило NAT, которое направляет весь входящий трафик с порта 21 на порт 22<sup>1</sup>;</span><span class="sxs-lookup"><span data-stu-id="8dc4e-140">a NAT rule to translate all incoming traffic on port 21 to port 22<sup>1</sup></span></span>
* <span data-ttu-id="8dc4e-141">правило NAT, которое направляет весь входящий трафик с порта 23 на порт 22;</span><span class="sxs-lookup"><span data-stu-id="8dc4e-141">a NAT rule to translate all incoming traffic on port 23 to port 22</span></span>
* <span data-ttu-id="8dc4e-142">правило балансировщика нагрузки, которое балансирует весь входящий трафик на порту 80, перенаправляя трафик на порт 80 других адресов во внутреннем пуле;</span><span class="sxs-lookup"><span data-stu-id="8dc4e-142">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="8dc4e-143">правило пробы, согласно которому будет проверяться состояние работоспособности на странице *HealthProbe.aspx*.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-143">a probe rule to check the health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="8dc4e-144"><sup>1</sup> Правила NAT сопоставлены с конкретным экземпляром виртуальной машины, находящимся в зоне действия балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-144"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="8dc4e-145">Сетевой трафик, поступающий на порт 21, отправляется в определенную виртуальную машину на порту 22, связанным с этим правилом NAT.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-145">The network traffic arriving on port 21 is sent to a specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="8dc4e-146">Для правила NAT необходимо указать протокол (UDP или TCP).</span><span class="sxs-lookup"><span data-stu-id="8dc4e-146">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="8dc4e-147">Нельзя назначить оба протокола одному и тому же порту.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-147">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="8dc4e-148">Создайте правила NAT.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-148">Create the NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="8dc4e-149">Создайте правило балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-149">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="8dc4e-150">Создайте пробу работоспособности.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-150">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="8dc4e-151">Проверьте параметры.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-151">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="8dc4e-152">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8dc4e-152">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up the load balancer "nrplb"
        + Looking up the public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a><span data-ttu-id="8dc4e-153">Создание сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="8dc4e-153">Create NICs</span></span>

<span data-ttu-id="8dc4e-154">Вам необходимо создать сетевые адаптеры (или изменить существующие) и связать их с правилами NAT, правилами балансировщика нагрузки и пробами.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="8dc4e-155">Создайте сетевую карту *lb-nic1-be* и свяжите ее с правилом NAT *rdp1*, а также с пулом внутренних адресов *NRPbackendpool*.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-155">Create a NIC named *lb-nic1-be*, and associate it with the *rdp1* NAT rule, and the *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="8dc4e-156">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8dc4e-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up the network interface "lb-nic1-be"
        + Looking up the subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up the network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="8dc4e-157">Создайте сетевую карту *lb-nic2-be* и свяжите ее с правилом NAT *rdp2*, а также с пулом внутренних адресов *NRPbackendpool*.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-157">Create a NIC named *lb-nic2-be*, and associate it with the *rdp2* NAT rule, and the *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="8dc4e-158">Создайте виртуальную машину *web1* и свяжите ее с сетевым адаптером *lb-nic1-be*.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-158">Create a virtual machine (VM) named *web1*, and associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="8dc4e-159">Учетная запись хранения *web1nrp* была создана перед выполнением следующей команды.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-159">A storage account called *web1nrp* was created before running the command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="8dc4e-160">Виртуальные машины в балансировщике нагрузки должны находиться в одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="8dc4e-161">Создайте группу доступности с помощью команды `azure availset create` .</span><span class="sxs-lookup"><span data-stu-id="8dc4e-161">Use `azure availset create` to create an availability set.</span></span>

    <span data-ttu-id="8dc4e-162">Должен быть получен результат, аналогичный приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="8dc4e-162">The output should be similar to the following:</span></span>

        info:    Executing command vm create
        + Looking up the VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using the VM Size "Standard_A1"
        info:    The [OS, Data] Disk or image configuration requires storage account
        + Looking up the storage account web1nrp
        + Looking up the availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up the NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in the NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="8dc4e-163">Информационное сообщение **В этой сетевой карте не настроен параметр publicIP** является ожидаемым, так как сетевая карта, созданная для балансировщика нагрузки, будет подключаться к Интернету через общедоступный IP-адрес балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-163">The informational message **This is a NIC without publicIP configured** is expected since the NIC created for the load balancer connecting to Internet using the load balancer public IP address.</span></span>

    <span data-ttu-id="8dc4e-164">Так как сетевой адаптер *lb-nic1-be* связан с правилом NAT *rdp1*, вы можете подключиться к виртуальной машине *web1* с помощью RDP через порт 3441 в балансировщике нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-164">Since the *lb-nic1-be* NIC is associated with the *rdp1* NAT rule, you can connect to *web1* using RDP through port 3441 on the load balancer.</span></span>

4. <span data-ttu-id="8dc4e-165">Создайте виртуальную машину *web2* и свяжите ее с сетевым адаптером *lb-nic2-be*.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-165">Create a virtual machine (VM) named *web2*, and associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="8dc4e-166">Учетная запись хранения *web1nrp* была создана перед выполнением следующей команды.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-166">A storage account called *web1nrp* was created before running the command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="8dc4e-167">Обновление существующего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="8dc4e-167">Update an existing load balancer</span></span>
<span data-ttu-id="8dc4e-168">Вы можете добавить правила, ссылающиеся на существующий балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-168">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="8dc4e-169">В следующем примере новое правило балансировщика нагрузки добавляется в существующий балансировщик нагрузки **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="8dc4e-169">In the next example, a new load balancer rule is added to an existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="8dc4e-170">Удаление балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="8dc4e-170">Delete a load balancer</span></span>
<span data-ttu-id="8dc4e-171">Чтобы удалить балансировщик нагрузки, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="8dc4e-171">Use the following command to remove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="8dc4e-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8dc4e-172">Next steps</span></span>
[<span data-ttu-id="8dc4e-173">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8dc4e-173">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="8dc4e-174">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8dc4e-174">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="8dc4e-175">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8dc4e-175">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
