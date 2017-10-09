---
title: "Подсистема балансировки - нагрузки на aaaCreate из Интернета, Azure CLI | Документы Microsoft"
description: "Узнайте, как toocreate с выходом подсистемы балансировки нагрузки Интернета с помощью диспетчера ресурсов hello Azure CLI"
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
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a><span data-ttu-id="8db49-103">Создание Интернет подсистемы балансировки нагрузки, с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8db49-103">Creating an internet load balancer using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8db49-104">Портал</span><span class="sxs-lookup"><span data-stu-id="8db49-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="8db49-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8db49-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="8db49-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8db49-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="8db49-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="8db49-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="8db49-108">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8db49-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="8db49-109">Вы также можете [Узнайте, как с помощью классического развертывания подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8db49-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="8db49-110">Развертывание решения hello, с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8db49-110">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="8db49-111">Привет, следующие шаги показывают, как с помощью диспетчера ресурсов Azure с CLI подсистемы балансировки нагрузки, toocreate из Интернета.</span><span class="sxs-lookup"><span data-stu-id="8db49-111">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="8db49-112">С помощью диспетчера ресурсов Azure создается и настраивается по отдельности каждого ресурса, затем объединить toocreate ресурса.</span><span class="sxs-lookup"><span data-stu-id="8db49-112">With Azure Resource Manager each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="8db49-113">Необходимо создать и настроить hello следующие объекты toodeploy подсистемы балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="8db49-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="8db49-114">Конфигурация интерфейсных IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="8db49-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="8db49-115">Пул адресов серверной части - содержит сетевых интерфейсов (NIC) для hello виртуальные машины tooreceive сетевой трафик от подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="8db49-115">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="8db49-116">Правила балансировки нагрузки — содержит правила сопоставления открытый порт hello tooport подсистемы балансировки нагрузки в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="8db49-116">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="8db49-117">Правила NAT для входящих подключений — содержит правила, сопоставление порта открытый порт tooa подсистемы балансировки нагрузки hello для конкретной виртуальной машины в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="8db49-117">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="8db49-118">Проверяет — содержит доступность toocheck проверки, используемые работоспособности экземпляров виртуальных машин в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="8db49-118">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="8db49-119">Дополнительные сведения см. в статье о [поддержке Azure Resource Manage для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8db49-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="8db49-120">Настройка toouse интерфейс командной строки диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="8db49-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="8db49-121">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="8db49-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="8db49-122">Запустите hello **azure конфигурации режима** tooswitch tooResource Manager режим команд, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8db49-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="8db49-123">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8db49-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="8db49-124">Создайте виртуальную сеть и общедоступный IP-адрес пула IP-интерфейса hello</span><span class="sxs-lookup"><span data-stu-id="8db49-124">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="8db49-125">Создание виртуальной сети (VNet) с именем *NRPVnet* Восток США там hello группу ресурсов с именем *NRPRG*.</span><span class="sxs-lookup"><span data-stu-id="8db49-125">Create a virtual network (VNet) named *NRPVnet* in hello East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="8db49-126">Создайте подсеть *NRPVnetSubnet* с блоком CIDR 10.0.0.0/24 в виртуальной сети *NRPVnet*.</span><span class="sxs-lookup"><span data-stu-id="8db49-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="8db49-127">Создать общедоступный IP-адрес с именем *NRPPublicIP* toobe, используемый пулом IP-интерфейса с именем DNS *loadbalancernrp.eastus.cloudapp.azure.com*. hello ниже используется тип статического выделения hello и тайм-аут простоя 4 минуты.</span><span class="sxs-lookup"><span data-stu-id="8db49-127">Create a public IP address named *NRPPublicIP* toobe used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*. hello command below uses hello static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="8db49-128">Hello балансировки нагрузки будет использовать метку hello общедоступный IP-адрес домена hello по полным доменным ИМЕНЕМ.</span><span class="sxs-lookup"><span data-stu-id="8db49-128">hello load balancer will use hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="8db49-129">Это изменение по сравнению с классической развертывания с использованием hello облачной службы как hello балансировки нагрузки полное доменное имя (FQDN).</span><span class="sxs-lookup"><span data-stu-id="8db49-129">This a change from classic deployment, which uses hello cloud service as hello load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="8db49-130">В этом примере hello полное доменное имя — *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="8db49-130">In this example, hello FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="8db49-131">Создание балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="8db49-131">Create a load balancer</span></span>

<span data-ttu-id="8db49-132">Hello следующая команда создает подсистемы балансировки нагрузки с именем *NRPlb* в hello *NRPRG* группы ресурсов в hello *Восток США* расположение Azure.</span><span class="sxs-lookup"><span data-stu-id="8db49-132">hello following command creates a load balancer named *NRPlb* in hello *NRPRG* resource group in hello *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="8db49-133">Создание пула интерфейсных IP-адресов и пула внутренних адресов</span><span class="sxs-lookup"><span data-stu-id="8db49-133">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="8db49-134">В этом примере демонстрируется toocreate hello переднего плана пула IP-адресов, получающий hello входящего сетевого трафика на hello подсистемы балансировки нагрузки и hello внутреннего пула IP-адресов, где переднего плана пула hello отправляет hello балансировки нагрузки сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="8db49-134">This example demonstrates how toocreate hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello backend IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="8db49-135">Создайте пул IP переднего плана, связывание hello общедоступный IP-адрес создан в предыдущем шаге hello и Подсистема балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="8db49-135">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="8db49-136">Настройте пул адресов серверной части используется tooreceive входящего трафика из пула IP-интерфейса hello.</span><span class="sxs-lookup"><span data-stu-id="8db49-136">Set up a back-end address pool used tooreceive incoming traffic from hello front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="8db49-137">Создание правил балансировки нагрузки, правил NAT и пробы</span><span class="sxs-lookup"><span data-stu-id="8db49-137">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="8db49-138">В этом примере создается hello следующих элементов.</span><span class="sxs-lookup"><span data-stu-id="8db49-138">This example creates hello following items.</span></span>

* <span data-ttu-id="8db49-139">правило NAT для tootranslate весь входящий трафик на порт 21 tooport 22<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="8db49-139">a NAT rule tootranslate all incoming traffic on port 21 tooport 22<sup>1</sup></span></span>
* <span data-ttu-id="8db49-140">правило NAT для tootranslate весь входящий трафик на порт 23 tooport 22</span><span class="sxs-lookup"><span data-stu-id="8db49-140">a NAT rule tootranslate all incoming traffic on port 23 tooport 22</span></span>
* <span data-ttu-id="8db49-141">toobalance правило балансировки нагрузки весь входящий трафик на порт 80 tooport 80 на hello адресов серверной части пула hello.</span><span class="sxs-lookup"><span data-stu-id="8db49-141">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="8db49-142">состояние проверки правила toocheck hello работоспособности на страницу с именем *HealthProbe.aspx*.</span><span class="sxs-lookup"><span data-stu-id="8db49-142">a probe rule toocheck hello health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="8db49-143"><sup>1</sup> NAT правила, связанные tooa конкретного экземпляра виртуальной машины за подсистемой балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="8db49-143"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="8db49-144">Hello сетевой трафик, поступающий на порт 21 отправляется tooa отдельную виртуальную машину на порт, связанный с этим правилом NAT 22.</span><span class="sxs-lookup"><span data-stu-id="8db49-144">hello network traffic arriving on port 21 is sent tooa specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="8db49-145">Для правила NAT необходимо указать протокол (UDP или TCP).</span><span class="sxs-lookup"><span data-stu-id="8db49-145">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="8db49-146">Оба эти протокола не может быть назначен toohello тот же порт.</span><span class="sxs-lookup"><span data-stu-id="8db49-146">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="8db49-147">Создание правил NAT hello.</span><span class="sxs-lookup"><span data-stu-id="8db49-147">Create hello NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="8db49-148">Создайте правило балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8db49-148">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="8db49-149">Создайте пробу работоспособности.</span><span class="sxs-lookup"><span data-stu-id="8db49-149">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="8db49-150">Проверьте параметры.</span><span class="sxs-lookup"><span data-stu-id="8db49-150">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="8db49-151">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8db49-151">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
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

## <a name="create-nics"></a><span data-ttu-id="8db49-152">Создание сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="8db49-152">Create NICs</span></span>

<span data-ttu-id="8db49-153">Необходима toocreate сетевые адаптеры (или изменить существующие) и связать их tooNAT правила, правила подсистемы балансировки нагрузки и зонды.</span><span class="sxs-lookup"><span data-stu-id="8db49-153">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="8db49-154">Создайте сетевую КАРТУ с именем *быть балансировки нагрузки сетевого адаптера 1*и связать его с hello *rdp1* NAT правило и hello *NRPbackendpool* пул адресов серверной части.</span><span class="sxs-lookup"><span data-stu-id="8db49-154">Create a NIC named *lb-nic1-be*, and associate it with hello *rdp1* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="8db49-155">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8db49-155">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
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

2. <span data-ttu-id="8db49-156">Создайте сетевую КАРТУ с именем *балансировки нагрузки nic2 быть*и связать его с hello *rdp2* NAT правило и hello *NRPbackendpool* пул адресов серверной части.</span><span class="sxs-lookup"><span data-stu-id="8db49-156">Create a NIC named *lb-nic2-be*, and associate it with hello *rdp2* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="8db49-157">Создание виртуальной машины (VM) с именем *web1*и связать его с сетевого Адаптера с именем hello *быть балансировки нагрузки сетевого адаптера 1*.</span><span class="sxs-lookup"><span data-stu-id="8db49-157">Create a virtual machine (VM) named *web1*, and associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="8db49-158">Вызывается учетной записи хранилища *web1nrp* была создана перед выполнением команды hello ниже.</span><span class="sxs-lookup"><span data-stu-id="8db49-158">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="8db49-159">Виртуальные машины в toobe необходимость подсистемы балансировки нагрузки, в hello одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="8db49-159">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="8db49-160">Используйте `azure availset create` toocreate набор доступности.</span><span class="sxs-lookup"><span data-stu-id="8db49-160">Use `azure availset create` toocreate an availability set.</span></span>

    <span data-ttu-id="8db49-161">Hello выходные данные должны быть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="8db49-161">hello output should be similar toohello following:</span></span>

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="8db49-162">Информационное сообщение Hello **это сетевой Адаптер без общедоступный IP-адрес настроен** ожидается с момента создания hello сетевой Адаптер для подключения tooInternet hello нагрузки балансировки общедоступный IP-адрес с помощью подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="8db49-162">hello informational message **This is a NIC without publicIP configured** is expected since hello NIC created for hello load balancer connecting tooInternet using hello load balancer public IP address.</span></span>

    <span data-ttu-id="8db49-163">С момента hello *быть балансировки нагрузки сетевого адаптера 1* сетевой Адаптер связан с hello *rdp1* правила NAT, можно подключить слишком*web1* с помощью протокола удаленного рабочего СТОЛА через порт 3441 в подсистеме балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="8db49-163">Since hello *lb-nic1-be* NIC is associated with hello *rdp1* NAT rule, you can connect too*web1* using RDP through port 3441 on hello load balancer.</span></span>

4. <span data-ttu-id="8db49-164">Создание виртуальной машины (VM) с именем *web2*и связать его с сетевого Адаптера с именем hello *балансировки нагрузки nic2 быть*.</span><span class="sxs-lookup"><span data-stu-id="8db49-164">Create a virtual machine (VM) named *web2*, and associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="8db49-165">Вызывается учетной записи хранилища *web1nrp* была создана перед выполнением команды hello ниже.</span><span class="sxs-lookup"><span data-stu-id="8db49-165">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="8db49-166">Обновление существующего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="8db49-166">Update an existing load balancer</span></span>
<span data-ttu-id="8db49-167">Вы можете добавить правила, ссылающиеся на существующий балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8db49-167">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="8db49-168">В следующем примере hello новое правило балансировки нагрузки добавляется существующей подсистемы балансировки нагрузки tooan **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="8db49-168">In hello next example, a new load balancer rule is added tooan existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="8db49-169">Удаление балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="8db49-169">Delete a load balancer</span></span>
<span data-ttu-id="8db49-170">Используйте hello, следующая команда tooremove подсистемы балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="8db49-170">Use hello following command tooremove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="8db49-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8db49-171">Next steps</span></span>
[<span data-ttu-id="8db49-172">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8db49-172">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="8db49-173">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8db49-173">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="8db49-174">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8db49-174">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
