---
title: "Балансировка нагрузки виртуальных машин Linux в Azure | Документы Майкрософт"
description: "Сведения о создании высокодоступного безопасного приложения, выполняемого на трех виртуальных машинах Linux с использованием Azure Load Balancer."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7b3a089d2f6386afcc46cbc4377594be0d758fc6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-linux-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="cc310-103">Балансировка нагрузки виртуальных машин Linux в Azure для создания высокодоступного приложения</span><span class="sxs-lookup"><span data-stu-id="cc310-103">How to load balance Linux virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="cc310-104">Балансировка нагрузки обеспечивает более высокий уровень доступности за счет распределения входящих запросов между несколькими виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="cc310-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="cc310-105">В этом руководстве вы узнаете о различных компонентах балансировщика нагрузки Azure Load Balancer, распределяющего трафик и обеспечивающего высокую доступность.</span><span class="sxs-lookup"><span data-stu-id="cc310-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="cc310-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="cc310-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cc310-107">Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="cc310-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="cc310-108">Создание пробы работоспособности балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="cc310-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="cc310-109">создавать правила трафика подсистемы балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="cc310-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="cc310-110">создавать базовое приложение Node.js с помощью файла конфигурации cloud-init;</span><span class="sxs-lookup"><span data-stu-id="cc310-110">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="cc310-111">создавать виртуальные машины и присоединять их к подсистеме балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="cc310-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="cc310-112">Просмотр балансировщика нагрузки в действии</span><span class="sxs-lookup"><span data-stu-id="cc310-112">View a load balancer in action</span></span>
> * <span data-ttu-id="cc310-113">добавлять и удалять виртуальные машины из подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc310-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cc310-114">Если вы решили установить и использовать интерфейс командной строки локально, то для работы с этим руководством вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="cc310-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cc310-115">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="cc310-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="cc310-116">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cc310-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="cc310-117">Обзор Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="cc310-117">Azure load balancer overview</span></span>
<span data-ttu-id="cc310-118">Azure Load Balancer представляет собой балансировщик нагрузки уровня 4 (TCP, UDP), который обеспечивает высокий уровень доступности, распределяя входящий трафик между работоспособными виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="cc310-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="cc310-119">Проба работоспособности позволяет отслеживать данный порт на каждой виртуальной машине и передавать трафик только в рабочую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="cc310-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="cc310-120">Вы определяете интерфейсную конфигурацию IP-адресов, содержащую один или несколько общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="cc310-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="cc310-121">Такая интерфейсная конфигурация IP-адресов предоставляет доступ к балансировщику нагрузки и приложениям через Интернет.</span><span class="sxs-lookup"><span data-stu-id="cc310-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="cc310-122">Виртуальные машины подключаются к балансировщику нагрузки с помощью виртуальной сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="cc310-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="cc310-123">Для распределения трафика между виртуальными машинами внутренний пул адресов содержит IP-адреса виртуальных сетевых карт, подключенных к балансировщику нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc310-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="cc310-124">Чтобы управлять потоком трафика, нужно определить правила балансировщика нагрузки для определенных портов и протоколов, сопоставленных с виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="cc310-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>

<span data-ttu-id="cc310-125">Если в предыдущем руководстве вы дошли до шага [Создание набора для масштабирования виртуальной машины](tutorial-create-vmss.md), балансировщик нагрузки должен быть уже создан.</span><span class="sxs-lookup"><span data-stu-id="cc310-125">If you followed the previous tutorial to [create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="cc310-126">Все эти компоненты были настроены в составе масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="cc310-126">All these components were configured for you as part of the scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="cc310-127">Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="cc310-127">Create Azure load balancer</span></span>
<span data-ttu-id="cc310-128">Этот раздел подробно описывает, как создать и настроить каждый из компонентов балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc310-128">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="cc310-129">Прежде чем создать балансировщик нагрузки, выполните команду [az group create](/cli/azure/group#create) для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cc310-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="cc310-130">В следующем примере создается группа ресурсов с именем *myResourceGroupLoadBalancer* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="cc310-130">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="cc310-131">Создание общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="cc310-131">Create a public IP address</span></span>
<span data-ttu-id="cc310-132">Для доступа к приложению через Интернет требуется общедоступный IP-адрес для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc310-132">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="cc310-133">Создайте общедоступный IP-адрес с помощью команды [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="cc310-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="cc310-134">В следующем примере создается общедоступный IP-адрес *myPublicIP* в группе ресурсов *myResourceGroupLoadBalancer*.</span><span class="sxs-lookup"><span data-stu-id="cc310-134">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="cc310-135">Создание балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="cc310-135">Create a load balancer</span></span>
<span data-ttu-id="cc310-136">Создайте балансировщик нагрузки с помощью команды [az network lb create](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="cc310-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="cc310-137">В следующем примере создается подсистема балансировки нагрузки *myLoadBalancer*, а адрес *myPublicIP* назначается внешней IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cc310-137">The following example creates a load balancer named *myLoadBalancer* and assigns the *myPublicIP* address to the front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="cc310-138">Создание пробы работоспособности</span><span class="sxs-lookup"><span data-stu-id="cc310-138">Create a health probe</span></span>
<span data-ttu-id="cc310-139">Чтобы балансировщик нагрузки мог следить за состоянием приложения, необходимо настроить пробу работоспособности.</span><span class="sxs-lookup"><span data-stu-id="cc310-139">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="cc310-140">Проба работоспособности динамически добавляет или удаляет виртуальные машины из балансировщика нагрузки на основе их ответа на проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="cc310-140">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="cc310-141">По умолчанию виртуальная машина удаляется из числа машин, на которые балансировщик распределяет нагрузку, после двух последовательных сбоев с интервалом в 15 секунд.</span><span class="sxs-lookup"><span data-stu-id="cc310-141">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="cc310-142">Пробу работоспособности можно создать на основе протокола или конкретной страницы проверки работоспособности приложения.</span><span class="sxs-lookup"><span data-stu-id="cc310-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="cc310-143">В следующем примере создается проба TCP.</span><span class="sxs-lookup"><span data-stu-id="cc310-143">The following example creates a TCP probe.</span></span> <span data-ttu-id="cc310-144">Вы также можете создать настраиваемую пробу HTTP для более детальных проверок.</span><span class="sxs-lookup"><span data-stu-id="cc310-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="cc310-145">При использовании настраиваемой пробы HTTP нужно создать страницу проверки работоспособности, например *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="cc310-145">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="cc310-146">Чтобы обеспечить работоспособность узла, проба должна возвращать ответ **HTTP 200 OK** для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc310-146">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="cc310-147">Чтобы создать пробу работоспособности TCP, используйте команду [az network lb probe create](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="cc310-147">To create a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="cc310-148">В следующем примере создается проба TCP *myHealthProbe*.</span><span class="sxs-lookup"><span data-stu-id="cc310-148">The following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="cc310-149">Создание правила балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="cc310-149">Create a load balancer rule</span></span>
<span data-ttu-id="cc310-150">Правило балансировщика нагрузки позволяет определить распределение трафика между виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="cc310-150">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="cc310-151">Вы определяете интерфейсную конфигурацию IP-адресов для входящего трафика и внутренний пул IP-адресов для приема трафика, а также требуемый порт источника и назначения.</span><span class="sxs-lookup"><span data-stu-id="cc310-151">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="cc310-152">Чтобы обеспечить получение трафика только работоспособными виртуальными машинами, можно также определить используемую пробу работоспособности.</span><span class="sxs-lookup"><span data-stu-id="cc310-152">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="cc310-153">Создайте правило балансировщика нагрузки с помощью команды [az network lb rule create](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="cc310-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="cc310-154">В следующем примере создается правило *myLoadBalancerRule*, используется проба работоспособности *myHealthProbe* и трафик распределяется через порт *80*.</span><span class="sxs-lookup"><span data-stu-id="cc310-154">The following example creates a rule named *myLoadBalancerRule*, uses the *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a><span data-ttu-id="cc310-155">Настройка виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="cc310-155">Configure virtual network</span></span>
<span data-ttu-id="cc310-156">Прежде чем развертывать виртуальные машины и тестировать балансировщик нагрузки, создайте вспомогательные ресурсы виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="cc310-156">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="cc310-157">Дополнительные сведения о виртуальных сетях см. в руководстве [Управление виртуальными сетями Azure](tutorial-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="cc310-157">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="cc310-158">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="cc310-158">Create network resources</span></span>
<span data-ttu-id="cc310-159">Создайте виртуальную сеть с помощью команды [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="cc310-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="cc310-160">В следующем примере создается виртуальная сеть *myVnet* с подсетью *mySubnet*.</span><span class="sxs-lookup"><span data-stu-id="cc310-160">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="cc310-161">Чтобы добавить группу безопасности сети, используйте команду [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="cc310-161">To add a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="cc310-162">В следующем примере создается группа безопасности сети *myNetworkSecurityGroup*.</span><span class="sxs-lookup"><span data-stu-id="cc310-162">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="cc310-163">Создайте правило группы безопасности сети с помощью команды [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="cc310-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="cc310-164">В следующем примере создается правило группы безопасности сети *myNetworkSecurityGroupRule*.</span><span class="sxs-lookup"><span data-stu-id="cc310-164">The following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="cc310-165">Для создания виртуальных сетевых карт используется команда [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="cc310-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="cc310-166">В следующем примере создаются три виртуальных сетевых адаптера</span><span class="sxs-lookup"><span data-stu-id="cc310-166">The following example creates three virtual NICs.</span></span> <span data-ttu-id="cc310-167">(по одной виртуальной сетевой карте для каждой виртуальной машины, используемой приложением).</span><span class="sxs-lookup"><span data-stu-id="cc310-167">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="cc310-168">Вы можете в любое время создать дополнительные виртуальные сетевые карты и виртуальные машины и добавить их в балансировщик нагрузки:</span><span class="sxs-lookup"><span data-stu-id="cc310-168">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a><span data-ttu-id="cc310-169">Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="cc310-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="cc310-170">Создание конфигурации cloud-init</span><span class="sxs-lookup"><span data-stu-id="cc310-170">Create cloud-init config</span></span>
<span data-ttu-id="cc310-171">В предыдущем руководстве [Как настроить виртуальную машину Linux при первой загрузке](tutorial-automate-vm-deployment.md) вы узнали, как автоматизировать настройку виртуальной машины с помощью cloud-init.</span><span class="sxs-lookup"><span data-stu-id="cc310-171">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="cc310-172">Тот же самый файл конфигурации cloud-init можно использовать и для установки NGINX, а также для запуска простого приложения Node.js "Hello World".</span><span class="sxs-lookup"><span data-stu-id="cc310-172">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="cc310-173">В текущей оболочке создайте файл *cloud-init.txt* и вставьте в него следующую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="cc310-173">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="cc310-174">Например, создайте файл в Cloud Shell, не на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="cc310-174">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="cc310-175">Введите `sensible-editor cloud-init.txt`, чтобы создать файл и просмотреть список доступных редакторов.</span><span class="sxs-lookup"><span data-stu-id="cc310-175">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="cc310-176">Убедитесь, что весь файл cloud-init скопирован правильно, особенно первая строка:</span><span class="sxs-lookup"><span data-stu-id="cc310-176">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a><span data-ttu-id="cc310-177">Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="cc310-177">Create virtual machines</span></span>
<span data-ttu-id="cc310-178">Чтобы улучшить высокую доступность приложения, поместите виртуальные машины в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="cc310-178">To improve the high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="cc310-179">Дополнительные сведения о группах доступности см. в руководстве [Создание высокодоступных виртуальных машин](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="cc310-179">For more information about availability sets, see the previous [How to create highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="cc310-180">Создайте группу доступности с помощью команды [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="cc310-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="cc310-181">В следующем примере создается группа доступности *myAvailabilitySet*.</span><span class="sxs-lookup"><span data-stu-id="cc310-181">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="cc310-182">Теперь вы можете создать виртуальные машины с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="cc310-182">Now you can create the VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="cc310-183">В следующем примере создаются три виртуальные машины и ключи SSH, если они не существуют.</span><span class="sxs-lookup"><span data-stu-id="cc310-183">The following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

<span data-ttu-id="cc310-184">Некоторые фоновые задачи продолжают работу после возврата к командной строке в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="cc310-184">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="cc310-185">Параметр `--no-wait` не ожидает завершения всех задач.</span><span class="sxs-lookup"><span data-stu-id="cc310-185">The `--no-wait` parameter does not wait for all the tasks to complete.</span></span> <span data-ttu-id="cc310-186">Прежде чем вы получите доступ к приложению, может пройти несколько минут.</span><span class="sxs-lookup"><span data-stu-id="cc310-186">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="cc310-187">Проба работоспособности балансировщика нагрузки автоматически определяет, когда приложение работает на каждой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="cc310-187">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="cc310-188">Как только приложение будет запущено, правило балансировщика нагрузки начнет распределение трафика.</span><span class="sxs-lookup"><span data-stu-id="cc310-188">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="cc310-189">Проверка балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="cc310-189">Test load balancer</span></span>
<span data-ttu-id="cc310-190">Получите общедоступный IP-адрес балансировщика нагрузки с помощью команды [az network public-ip show](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="cc310-190">Obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="cc310-191">Следующий пример позволяет получить IP-адрес для созданного ранее *myPublicIP*.</span><span class="sxs-lookup"><span data-stu-id="cc310-191">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="cc310-192">После этого можно ввести общедоступный IP-адрес в веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="cc310-192">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="cc310-193">Помните, прежде чем подсистема балансировки нагрузки начнет распределять трафик между виртуальными машинами, виртуальные машины должны быть подготовлены. Эта подготовка может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="cc310-193">Remember - it takes a few minutes the the VMs to be ready before the load balancer starts to distribute traffic to them.</span></span> <span data-ttu-id="cc310-194">Отображается приложение, а также имя узла виртуальной машины, на которую балансировщик нагрузки направил трафик, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="cc310-194">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Запуск приложения Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="cc310-196">Чтобы увидеть, как балансировщик нагрузки распределяет трафик между тремя виртуальными машинами, на которых выполняется приложение, принудительно обновите веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="cc310-196">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="cc310-197">Добавление и удаление виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="cc310-197">Add and remove VMs</span></span>
<span data-ttu-id="cc310-198">На виртуальных машинах, выполняющих приложение, может потребоваться выполнить обслуживание, например установить обновления операционной системы.</span><span class="sxs-lookup"><span data-stu-id="cc310-198">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="cc310-199">Для обработки большего объема трафика в приложении необходимо добавить дополнительные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="cc310-199">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="cc310-200">В этом разделе показано, как удалить или добавить виртуальную машину из балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc310-200">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="cc310-201">Удаление виртуальной машины из балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="cc310-201">Remove a VM from the load balancer</span></span>
<span data-ttu-id="cc310-202">Вы можете удалить виртуальную машину из внутреннего пула адресов с помощью команды [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="cc310-202">You can remove a VM from the backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="cc310-203">В следующем примере из *myLoadBalancer* удаляется виртуальная сетевая карта для **myVM2**.</span><span class="sxs-lookup"><span data-stu-id="cc310-203">The following example removes the virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="cc310-204">Чтобы увидеть, как балансировщик нагрузки распределяет трафик между оставшимися двумя виртуальными машинами, на которых выполняется приложение, принудительно обновите веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="cc310-204">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="cc310-205">Теперь можно выполнить обслуживание на виртуальной машине, например установить обновления операционной системы или перезагрузить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="cc310-205">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="cc310-206">Добавление виртуальной машины в балансировщик нагрузки</span><span class="sxs-lookup"><span data-stu-id="cc310-206">Add a VM to the load balancer</span></span>
<span data-ttu-id="cc310-207">После выполнения обслуживания виртуальной машины, или если необходимо расширить емкость, можно добавить виртуальную машину во внутренний пул адресов с помощью команды [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="cc310-207">After performing VM maintenance, or if you need to expand capacity, you can add a VM to the backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="cc310-208">В следующем примере в *myLoadBalancer* добавляется виртуальная сетевая карта для **myVM2**.</span><span class="sxs-lookup"><span data-stu-id="cc310-208">The following example adds the virtual NIC for **myVM2** to *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="cc310-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc310-209">Next steps</span></span>
<span data-ttu-id="cc310-210">В рамках этого руководства вы создали балансировщик нагрузки и присоединили к нему виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="cc310-210">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="cc310-211">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="cc310-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cc310-212">Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="cc310-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="cc310-213">Создание пробы работоспособности балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="cc310-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="cc310-214">создавать правила трафика подсистемы балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="cc310-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="cc310-215">создавать базовое приложение Node.js с помощью файла конфигурации cloud-init;</span><span class="sxs-lookup"><span data-stu-id="cc310-215">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="cc310-216">создавать виртуальные машины и присоединять их к подсистеме балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="cc310-216">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="cc310-217">Просмотр балансировщика нагрузки в действии</span><span class="sxs-lookup"><span data-stu-id="cc310-217">View a load balancer in action</span></span>
> * <span data-ttu-id="cc310-218">добавлять и удалять виртуальные машины из подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc310-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="cc310-219">Для получения дополнительных сведений о компонентах виртуальных сетей Azure перейдите к указанному ниже руководству.</span><span class="sxs-lookup"><span data-stu-id="cc310-219">Advance to the next tutorial to learn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc310-220">Управление виртуальными сетями Azure и виртуальными машинами Linux с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cc310-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
