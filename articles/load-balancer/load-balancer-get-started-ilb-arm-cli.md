---
title: "Создание внутренней подсистемы балансировки нагрузки с помощью Azure CLI | Документация Майкрософт"
description: "Узнайте, как создать внутренний балансировщик нагрузки в Resource Manager с помощью Azure CLI."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 128b91c685b5f7e494a69ca5b04165a0ee7cbb78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-by-using-the-azure-cli"></a><span data-ttu-id="44054-103">Создание внутреннего балансировщика нагрузки с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="44054-103">Create an internal load balancer by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="44054-104">портале Azure</span><span class="sxs-lookup"><span data-stu-id="44054-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="44054-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="44054-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="44054-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="44054-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="44054-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="44054-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="44054-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="44054-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="44054-109">В этой статье описывается использование модели развертывания c помощью Resource Manager. Для большинства новых развертываний мы рекомендуем использовать эту модель вместо [классической](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="44054-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-solution-by-using-the-azure-cli"></a><span data-ttu-id="44054-110">Развертывание решения с помощью интерфейса командной строки Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="44054-110">Deploy the solution by using the Azure CLI</span></span>

<span data-ttu-id="44054-111">Ниже описана процедура создания балансировщика нагрузки для Интернета с помощью Azure Resource Manager и интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="44054-111">The following steps show how to create an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="44054-112">Azure Resource Manager позволяет по отдельности создавать и настраивать ресурсы, после чего на их основе создается единый ресурс.</span><span class="sxs-lookup"><span data-stu-id="44054-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="44054-113">Чтобы развернуть балансировщик нагрузки, необходимо создать и настроить следующие объекты:</span><span class="sxs-lookup"><span data-stu-id="44054-113">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="44054-114">**Конфигурация интерфейсных IP-адресов**: содержит общедоступные IP-адреса для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="44054-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="44054-115">**Пул внутренних адресов**: содержит сетевые интерфейсы (сетевые карты), которые позволяют виртуальным машинам получать трафик от балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="44054-115">**Back-end address pool**: contains network interfaces (NICs) that enable the virtual machines to receive network traffic from the load balancer</span></span>
* <span data-ttu-id="44054-116">**Правила балансировки нагрузки**: содержат правила сопоставления общего порта в балансировщике нагрузки с портом в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="44054-116">**Load-balancing rules**: contains rules that map a public port on the load balancer to port in the back-end address pool</span></span>
* <span data-ttu-id="44054-117">**Правила NAT для входящего трафика**: содержат правила сопоставления общего порта в балансировщике нагрузки с портом на конкретной виртуальной машине в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="44054-117">**Inbound NAT rules**: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool</span></span>
* <span data-ttu-id="44054-118">**Пробы**: содержат пробы работоспособности, которые используются для проверки доступности экземпляров виртуальных машин в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="44054-118">**Probes**: contains health probes that are used to check the availability of virtual machines instances in the back-end address pool</span></span>

<span data-ttu-id="44054-119">Дополнительные сведения см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="44054-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="44054-120">Настройка интерфейса командной строки для использования Resource Manager</span><span class="sxs-lookup"><span data-stu-id="44054-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="44054-121">Если вы никогда не использовали Azure CLI, см. статью [Установка Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="44054-121">If you have never used Azure CLI, see [Install and configure the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="44054-122">Следуйте инструкциям до того момента, где выбираются учетная запись и подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="44054-122">Follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="44054-123">Выполните команду **azure config mode** , чтобы переключиться в режим Resource Manager, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="44054-123">Run the **azure config mode** command to switch to Resource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="44054-124">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="44054-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="44054-125">Пошаговая инструкция по созданию внутреннего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="44054-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="44054-126">Войдите в Azure.</span><span class="sxs-lookup"><span data-stu-id="44054-126">Sign in to Azure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="44054-127">При появлении запроса введите свои учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="44054-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="44054-128">Измените командные инструменты на режим Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="44054-128">Change the command tools to Azure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="44054-129">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="44054-129">Create a resource group</span></span>

<span data-ttu-id="44054-130">Все ресурсы в Azure Resource Manager связаны с группой ресурсов.</span><span class="sxs-lookup"><span data-stu-id="44054-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="44054-131">Если вы еще этого не сделали, создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="44054-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="44054-132">Создание набора внутренних балансировщиков нагрузки</span><span class="sxs-lookup"><span data-stu-id="44054-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="44054-133">Создание внутреннего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="44054-133">Create an internal load balancer</span></span>

    <span data-ttu-id="44054-134">В следующем сценарии группа ресурсов с именем nrprg создается в восточном регионе США.</span><span class="sxs-lookup"><span data-stu-id="44054-134">In the following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="44054-135">Все ресурсы для внутреннего балансировщика нагрузки, такие как виртуальные сети и подсети виртуальных сетей, должны находиться в той же группе ресурсов и в том же регионе.</span><span class="sxs-lookup"><span data-stu-id="44054-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in the same resource group and in the same region.</span></span>

2. <span data-ttu-id="44054-136">Создайте интерфейсный IP-адрес для внутреннего балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="44054-136">Create a front-end IP address for the internal load balancer.</span></span>

    <span data-ttu-id="44054-137">Используемый IP-адрес должен быть в диапазоне подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="44054-137">The IP address that you use must be within the subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="44054-138">Создайте пул внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="44054-138">Create the back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="44054-139">После определения интерфейсного IP-адреса и пула внутренних адресов можно создать правила балансировщика нагрузки, правила NAT для входящего трафика и настроенные пробы работоспособности.</span><span class="sxs-lookup"><span data-stu-id="44054-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="44054-140">Создайте правило балансировщика нагрузки для внутреннего балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="44054-140">Create a load balancer rule for the internal load balancer.</span></span>

    <span data-ttu-id="44054-141">Во время выполнения описанных выше действий команда создает правило балансировщика нагрузки для прослушивания порта 1433 в интерфейсном пуле и отправки сетевого трафика со сбалансированной нагрузкой во внутренний пул адресов, также используя порт 1433.</span><span class="sxs-lookup"><span data-stu-id="44054-141">When you follow the previous steps, the command creates a load-balancer rule for listening to port 1433 in the front-end pool and sending load-balanced network traffic to the back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="44054-142">Создайте правило NAT для входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="44054-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="44054-143">Правила NAT для входящего трафика используются для создания конечных точек в балансировщике нагрузки, которые будут направлены к конкретному экземпляру виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="44054-143">Inbound NAT rules are used to create endpoints in a load balancer that go to a specific virtual machine instance.</span></span> <span data-ttu-id="44054-144">Предыдущие действия создали два правила NAT для удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="44054-144">The previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="44054-145">Создайте пробы работоспособности для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="44054-145">Create health probes for the load balancer.</span></span>

    <span data-ttu-id="44054-146">Проба работоспособности проверяет все экземпляры виртуальной машины, чтобы убедиться, что они могут отправлять сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="44054-146">A health probe checks all virtual machine instances to make sure they can send network traffic.</span></span> <span data-ttu-id="44054-147">Экземпляр виртуальной машины с неудачной пробой удаляется из балансировщика нагрузки, пока не перейдет в оперативный режим и проба не определит его работоспособность.</span><span class="sxs-lookup"><span data-stu-id="44054-147">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="44054-148">Для различных сценариев администрирования платформа Microsoft Azure использует статические общедоступные маршрутизируемые IPv4-адреса.</span><span class="sxs-lookup"><span data-stu-id="44054-148">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="44054-149">IP-адрес — 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="44054-149">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="44054-150">Не блокируйте этот IP-адрес брандмауэрами, поскольку это может привести к непредвиденному поведению.</span><span class="sxs-lookup"><span data-stu-id="44054-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="44054-151">Во внутреннем балансировщике нагрузки Azure этот IP-адрес используется пробами мониторинга для определения состояния работоспособности виртуальных машин в наборе балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="44054-151">With respect to Azure internal load balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="44054-152">Если группа безопасности сети используется для ограничения трафика, поступающего на виртуальные машины Azure в наборе внутренней балансировки нагрузки, или если она применяется к подсети виртуальной сети, то убедитесь в наличии правила сетевой безопасности, разрешающего поступление сетевого трафика с адреса 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="44054-152">If a network security group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a virtual network subnet, ensure that a network security rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="44054-153">Создание сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="44054-153">Create NICs</span></span>

<span data-ttu-id="44054-154">Вам необходимо создать сетевые адаптеры (или изменить существующие) и связать их с правилами NAT, правилами балансировщика нагрузки и пробами.</span><span class="sxs-lookup"><span data-stu-id="44054-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="44054-155">Создайте сетевую карту *lb-nic1-be*, а затем свяжите ее с правилом NAT *rdp1* и внутренним пулом адресов *beilb*.</span><span class="sxs-lookup"><span data-stu-id="44054-155">Create an NIC named *lb-nic1-be*, and then associate it with the *rdp1* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="44054-156">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="44054-156">Expected output:</span></span>

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

2. <span data-ttu-id="44054-157">Создайте сетевую карту *lb-nic2-be*, а затем свяжите ее с правилом NAT *rdp2* и внутренним пулом адресов *beilb*.</span><span class="sxs-lookup"><span data-stu-id="44054-157">Create an NIC named *lb-nic2-be*, and then associate it with the *rdp2* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="44054-158">Создайте виртуальную машину *DB1*, а затем свяжите ее с сетевой картой *lb-nic1-be*.</span><span class="sxs-lookup"><span data-stu-id="44054-158">Create a virtual machine named *DB1*, and then associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="44054-159">Учетная запись хранения *web1nrp* создается перед выполнением следующей команды:</span><span class="sxs-lookup"><span data-stu-id="44054-159">A storage account called *web1nrp* is created before the following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="44054-160">Виртуальные машины в балансировщике нагрузки должны находиться в одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="44054-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="44054-161">Создайте группу доступности с помощью команды `azure availset create` .</span><span class="sxs-lookup"><span data-stu-id="44054-161">Use `azure availset create` to create an availability set.</span></span>

4. <span data-ttu-id="44054-162">Создайте виртуальную машину *DB2*, а затем свяжите ее с сетевой картой *lb-nic2-be*.</span><span class="sxs-lookup"><span data-stu-id="44054-162">Create a virtual machine (VM) named *DB2*, and then associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="44054-163">Учетная запись хранения *web1nrp* была создана перед выполнением следующей команды:</span><span class="sxs-lookup"><span data-stu-id="44054-163">A storage account called *web1nrp* was created before running the following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="44054-164">Удаление балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="44054-164">Delete a load balancer</span></span>

<span data-ttu-id="44054-165">Чтобы удалить балансировщик нагрузки, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="44054-165">To remove a load balancer, use the following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="44054-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44054-166">Next steps</span></span>

[<span data-ttu-id="44054-167">Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу</span><span class="sxs-lookup"><span data-stu-id="44054-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="44054-168">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="44054-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

