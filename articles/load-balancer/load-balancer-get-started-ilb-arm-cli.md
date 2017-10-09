---
title: "Внутренний aaaCreate загрузить балансировки - Azure CLI | Документы Microsoft"
description: "Узнайте, как toocreate внутренняя Подсистема балансировки нагрузки с помощью hello Azure CLI в диспетчере ресурсов"
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
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a><span data-ttu-id="9da95-103">Создание внутренней подсистемы балансировки нагрузки с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9da95-103">Create an internal load balancer by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9da95-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="9da95-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="9da95-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9da95-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="9da95-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="9da95-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="9da95-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="9da95-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="9da95-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9da95-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="9da95-109">В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9da95-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a><span data-ttu-id="9da95-110">Развертывание решения hello с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9da95-110">Deploy hello solution by using hello Azure CLI</span></span>

<span data-ttu-id="9da95-111">Привет, следующие шаги показывают, как toocreate из Интернета подсистемы балансировки нагрузки с помощью диспетчера ресурсов Azure с CLI.</span><span class="sxs-lookup"><span data-stu-id="9da95-111">hello following steps show how toocreate an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="9da95-112">С помощью диспетчера ресурсов Azure каждый ресурс создается и настроить отдельно и затем поместить toocreate ресурса.</span><span class="sxs-lookup"><span data-stu-id="9da95-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="9da95-113">Требуется toocreate и настроить hello следующие объекты toodeploy подсистемы балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="9da95-113">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="9da95-114">**Конфигурация интерфейсных IP-адресов**: содержит общедоступные IP-адреса для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="9da95-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="9da95-115">**Пул адресов серверной части**: содержит сетевых интерфейсов (NIC), позволяющие hello виртуальные машины tooreceive сетевой трафик от подсистемы балансировки нагрузки hello</span><span class="sxs-lookup"><span data-stu-id="9da95-115">**Back-end address pool**: contains network interfaces (NICs) that enable hello virtual machines tooreceive network traffic from hello load balancer</span></span>
* <span data-ttu-id="9da95-116">**Правила балансировки нагрузки**: содержит правила, которые сопоставляют открытый порт hello tooport подсистемы балансировки нагрузки в пул адресов серверной части hello</span><span class="sxs-lookup"><span data-stu-id="9da95-116">**Load-balancing rules**: contains rules that map a public port on hello load balancer tooport in hello back-end address pool</span></span>
* <span data-ttu-id="9da95-117">**Правила NAT для входящих подключений**: содержит правила, которые сопоставляют открытый порт на порт tooa подсистемы балансировки нагрузки hello для конкретной виртуальной машины в пул адресов серверной части hello</span><span class="sxs-lookup"><span data-stu-id="9da95-117">**Inbound NAT rules**: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool</span></span>
* <span data-ttu-id="9da95-118">**Проверяет**: содержит проверках работоспособности, доступности hello используется toocheck экземпляров виртуальных машин в пул адресов серверной части hello</span><span class="sxs-lookup"><span data-stu-id="9da95-118">**Probes**: contains health probes that are used toocheck hello availability of virtual machines instances in hello back-end address pool</span></span>

<span data-ttu-id="9da95-119">Дополнительные сведения см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9da95-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="9da95-120">Настройка toouse интерфейс командной строки диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="9da95-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="9da95-121">Если ранее не пользовались Azure CLI, см. раздел [установить и настроить hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9da95-121">If you have never used Azure CLI, see [Install and configure hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="9da95-122">Следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="9da95-122">Follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="9da95-123">Запустите hello **azure конфигурации режима** команды режим Manager tooResource tooswitch, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9da95-123">Run hello **azure config mode** command tooswitch tooResource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="9da95-124">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9da95-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="9da95-125">Пошаговая инструкция по созданию внутреннего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="9da95-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="9da95-126">Войдите в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9da95-126">Sign in tooAzure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="9da95-127">При появлении запроса введите свои учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="9da95-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="9da95-128">Изменение режима средства tooAzure диспетчера ресурсов для hello команды.</span><span class="sxs-lookup"><span data-stu-id="9da95-128">Change hello command tools tooAzure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="9da95-129">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="9da95-129">Create a resource group</span></span>

<span data-ttu-id="9da95-130">Все ресурсы в Azure Resource Manager связаны с группой ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9da95-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="9da95-131">Если вы еще этого не сделали, создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9da95-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="9da95-132">Создание набора внутренних балансировщиков нагрузки</span><span class="sxs-lookup"><span data-stu-id="9da95-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="9da95-133">Создание внутреннего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="9da95-133">Create an internal load balancer</span></span>

    <span data-ttu-id="9da95-134">В следующие сценарии hello группу ресурсов с именем nrprg создается в регионе Восток США.</span><span class="sxs-lookup"><span data-stu-id="9da95-134">In hello following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="9da95-135">Все ресурсы для внутренних подсистем балансировки нагрузки, таких как виртуальные сети и подсети виртуальной сети должен быть в hello одну группу ресурсов и в hello же области.</span><span class="sxs-lookup"><span data-stu-id="9da95-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in hello same resource group and in hello same region.</span></span>

2. <span data-ttu-id="9da95-136">Создание внешнего IP-адреса для hello внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9da95-136">Create a front-end IP address for hello internal load balancer.</span></span>

    <span data-ttu-id="9da95-137">Hello IP-адреса, используемого должно быть в диапазоне подсети hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9da95-137">hello IP address that you use must be within hello subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="9da95-138">Создайте пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-138">Create hello back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="9da95-139">После определения интерфейсного IP-адреса и пула внутренних адресов можно создать правила балансировщика нагрузки, правила NAT для входящего трафика и настроенные пробы работоспособности.</span><span class="sxs-lookup"><span data-stu-id="9da95-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="9da95-140">Создайте правило подсистемы балансировки нагрузки для hello внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9da95-140">Create a load balancer rule for hello internal load balancer.</span></span>

    <span data-ttu-id="9da95-141">При выполнении предыдущего действия hello hello команда создает правило балансировки нагрузки для прослушивания tooport 1433 в пуле переднего плана hello и отправки балансировки нагрузки трафика toohello внутренней пул сетевых адресов, также использует порт 1433.</span><span class="sxs-lookup"><span data-stu-id="9da95-141">When you follow hello previous steps, hello command creates a load-balancer rule for listening tooport 1433 in hello front-end pool and sending load-balanced network traffic toohello back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="9da95-142">Создайте правило NAT для входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="9da95-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="9da95-143">Правила для входящих подключений NAT, используется toocreate конечные точки в подсистему балансировки нагрузки, go tooa конкретного экземпляра виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9da95-143">Inbound NAT rules are used toocreate endpoints in a load balancer that go tooa specific virtual machine instance.</span></span> <span data-ttu-id="9da95-144">предыдущие шаги Hello создать два правила NAT для удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="9da95-144">hello previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="9da95-145">Создайте пробы работоспособности подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-145">Create health probes for hello load balancer.</span></span>

    <span data-ttu-id="9da95-146">Проверка работоспособности проверяет все toomake экземпляров виртуальной машины, убедиться, что они могут отправлять сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="9da95-146">A health probe checks all virtual machine instances toomake sure they can send network traffic.</span></span> <span data-ttu-id="9da95-147">Hello экземпляр виртуальной машины с проверками сбоя проверки удаляется из hello балансировки нагрузки, пока не переходит в оперативный режим и проверку выборки определяет, что он исправен.</span><span class="sxs-lookup"><span data-stu-id="9da95-147">hello virtual machine instance with failed probe checks is removed from hello load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="9da95-148">Hello платформы Microsoft Azure использует статические публично маршрутизируемый IPv4-адрес для различных сценариев администрирования.</span><span class="sxs-lookup"><span data-stu-id="9da95-148">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="9da95-149">Hello IP-адрес — 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="9da95-149">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="9da95-150">Не блокируйте этот IP-адрес брандмауэрами, поскольку это может привести к непредвиденному поведению.</span><span class="sxs-lookup"><span data-stu-id="9da95-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="9da95-151">С учетом tooAzure внутренней балансировки нагрузки, отслеживая проб из состояние работоспособности hello toodetermine подсистемы балансировки нагрузки hello для виртуальных машин в набор балансировки нагрузки используется этот IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="9da95-151">With respect tooAzure internal load balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="9da95-152">Если группа безопасности сети является используется toorestrict трафика tooAzure виртуальные машины в наборе внутренне балансировки нагрузки или примененных tooa подсети виртуальной сети, убедитесь, что правило сетевой безопасности добавлен tooallow трафика из 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="9da95-152">If a network security group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa virtual network subnet, ensure that a network security rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="9da95-153">Создание сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="9da95-153">Create NICs</span></span>

<span data-ttu-id="9da95-154">Необходима toocreate сетевые адаптеры (или изменить существующие) и связать их tooNAT правила, правила подсистемы балансировки нагрузки и зонды.</span><span class="sxs-lookup"><span data-stu-id="9da95-154">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="9da95-155">Создание сетевого Адаптера с именем *быть балансировки нагрузки сетевого адаптера 1*и затем связать его с hello *rdp1* NAT правило и hello *beilb* пул адресов серверной части.</span><span class="sxs-lookup"><span data-stu-id="9da95-155">Create an NIC named *lb-nic1-be*, and then associate it with hello *rdp1* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="9da95-156">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9da95-156">Expected output:</span></span>

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

2. <span data-ttu-id="9da95-157">Создание сетевого Адаптера с именем *балансировки нагрузки nic2 быть*и затем связать его с hello *rdp2* NAT правило и hello *beilb* пул адресов серверной части.</span><span class="sxs-lookup"><span data-stu-id="9da95-157">Create an NIC named *lb-nic2-be*, and then associate it with hello *rdp2* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="9da95-158">Создание виртуальной машины с именем *DB1*и затем связать его с сетевого Адаптера с именем hello *быть балансировки нагрузки сетевого адаптера 1*.</span><span class="sxs-lookup"><span data-stu-id="9da95-158">Create a virtual machine named *DB1*, and then associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="9da95-159">Вызывается учетной записи хранилища *web1nrp* создан, прежде чем hello, следующая команда запускает:</span><span class="sxs-lookup"><span data-stu-id="9da95-159">A storage account called *web1nrp* is created before hello following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="9da95-160">Виртуальные машины в toobe необходимость подсистемы балансировки нагрузки, в hello одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="9da95-160">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="9da95-161">Используйте `azure availset create` toocreate набор доступности.</span><span class="sxs-lookup"><span data-stu-id="9da95-161">Use `azure availset create` toocreate an availability set.</span></span>

4. <span data-ttu-id="9da95-162">Создание виртуальной машины (VM) с именем *DB2*и затем связать его с сетевого Адаптера с именем hello *балансировки нагрузки nic2 быть*.</span><span class="sxs-lookup"><span data-stu-id="9da95-162">Create a virtual machine (VM) named *DB2*, and then associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="9da95-163">Вызывается учетной записи хранилища *web1nrp* была создана перед запуском hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="9da95-163">A storage account called *web1nrp* was created before running hello following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="9da95-164">Удаление балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="9da95-164">Delete a load balancer</span></span>

<span data-ttu-id="9da95-165">tooremove балансировщик нагрузки hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9da95-165">tooremove a load balancer, use hello following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="9da95-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9da95-166">Next steps</span></span>

[<span data-ttu-id="9da95-167">Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу</span><span class="sxs-lookup"><span data-stu-id="9da95-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="9da95-168">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="9da95-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

