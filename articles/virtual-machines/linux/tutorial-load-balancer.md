---
title: "aaaHow tooload сбалансировать виртуальных машин Linux в Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure распределять балансировки toocreate высокой доступности и безопасности приложений в трех виртуальных машин Linux"
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
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="5048e-103">Как tooload сбалансировать виртуальных машин Linux в Azure toocreate приложение с высокой доступностью</span><span class="sxs-lookup"><span data-stu-id="5048e-103">How tooload balance Linux virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="5048e-104">Балансировка нагрузки обеспечивает более высокий уровень доступности за счет распределения входящих запросов между несколькими виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="5048e-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="5048e-105">В этом учебнике вы узнаете о hello различных компонентов подсистемы балансировки нагрузки Azure hello, распределения трафика и обеспечения высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="5048e-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="5048e-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="5048e-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5048e-107">Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5048e-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="5048e-108">Создание пробы работоспособности балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="5048e-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="5048e-109">создавать правила трафика подсистемы балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="5048e-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="5048e-110">Использование облака init toocreate простое приложение Node.js</span><span class="sxs-lookup"><span data-stu-id="5048e-110">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="5048e-111">Создание виртуальных машин и присоединения tooa балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="5048e-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="5048e-112">Просмотр балансировщика нагрузки в действии</span><span class="sxs-lookup"><span data-stu-id="5048e-112">View a load balancer in action</span></span>
> * <span data-ttu-id="5048e-113">добавлять и удалять виртуальные машины из подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5048e-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5048e-114">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5048e-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5048e-115">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="5048e-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5048e-116">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5048e-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="5048e-117">Обзор Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5048e-117">Azure load balancer overview</span></span>
<span data-ttu-id="5048e-118">Azure Load Balancer представляет собой балансировщик нагрузки уровня 4 (TCP, UDP), который обеспечивает высокий уровень доступности, распределяя входящий трафик между работоспособными виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="5048e-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="5048e-119">Отслеживает данный порт на каждой виртуальной Машине зонда работоспособности подсистемы балансировки нагрузки и только распределяет трафик tooan оперативной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5048e-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="5048e-120">Вы определяете интерфейсную конфигурацию IP-адресов, содержащую один или несколько общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="5048e-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="5048e-121">Эту интерфейсный IP-конфигурацию позволяет вашей toobe нагрузки балансировки и приложения доступны через Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="5048e-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="5048e-122">Виртуальные машины подключены tooa подсистемы балансировки нагрузки с помощью их виртуальный сетевой адаптер (NIC).</span><span class="sxs-lookup"><span data-stu-id="5048e-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="5048e-123">toodistribute toohello трафика виртуальных машин, пул адресов серверной части содержит IP-адреса hello hello виртуальный (NIC) подключенных toohello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5048e-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="5048e-124">toocontrol hello потока трафика, определить правила подсистемы балансировки нагрузки для определенных портов и протоколов, сопоставить виртуальные машины tooyour.</span><span class="sxs-lookup"><span data-stu-id="5048e-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>

<span data-ttu-id="5048e-125">Если вы следовали предыдущим учебником hello слишком[создания набора масштабирования виртуальных машин](tutorial-create-vmss.md), подсистемы балансировки нагрузки будет создан.</span><span class="sxs-lookup"><span data-stu-id="5048e-125">If you followed hello previous tutorial too[create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="5048e-126">Все эти компоненты были настроены для вас в качестве части набора масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="5048e-126">All these components were configured for you as part of hello scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="5048e-127">Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5048e-127">Create Azure load balancer</span></span>
<span data-ttu-id="5048e-128">В этом разделе описаны создание и настройка каждого компонента балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="5048e-128">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="5048e-129">Прежде чем создать балансировщик нагрузки, выполните команду [az group create](/cli/azure/group#create) для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5048e-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="5048e-130">Hello следующий пример создает группу ресурсов с именем *myResourceGroupLoadBalancer* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="5048e-130">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="5048e-131">Создание общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="5048e-131">Create a public IP address</span></span>
<span data-ttu-id="5048e-132">tooaccess приложения на Здравствуйте Интернет, необходимые для балансировки нагрузки hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5048e-132">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="5048e-133">Создайте общедоступный IP-адрес с помощью команды [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="5048e-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="5048e-134">Hello следующий пример создает общедоступный IP-адрес с именем *myPublicIP* в hello *myResourceGroupLoadBalancer* группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="5048e-134">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="5048e-135">Создание балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="5048e-135">Create a load balancer</span></span>
<span data-ttu-id="5048e-136">Создайте балансировщик нагрузки с помощью команды [az network lb create](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="5048e-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="5048e-137">Hello следующий пример создает подсистемы балансировки нагрузки с именем *myLoadBalancer* и назначает hello *myPublicIP* адрес toohello интерфейсный IP-конфигурации:</span><span class="sxs-lookup"><span data-stu-id="5048e-137">hello following example creates a load balancer named *myLoadBalancer* and assigns hello *myPublicIP* address toohello front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="5048e-138">Создание пробы работоспособности</span><span class="sxs-lookup"><span data-stu-id="5048e-138">Create a health probe</span></span>
<span data-ttu-id="5048e-139">tooallow hello балансировки toomonitor hello состояние загрузки приложения, используйте проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="5048e-139">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="5048e-140">Проверка работоспособности Hello динамически добавляет или удаляет виртуальные машины из ротации подсистемы балансировки нагрузки hello, в зависимости от их проверки toohealth ответа.</span><span class="sxs-lookup"><span data-stu-id="5048e-140">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="5048e-141">По умолчанию виртуальная машина удаляется из распределения подсистемы балансировки нагрузки hello после двух последовательных сбоев каждые 15 секунд.</span><span class="sxs-lookup"><span data-stu-id="5048e-141">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="5048e-142">Пробу работоспособности можно создать на основе протокола или конкретной страницы проверки работоспособности приложения.</span><span class="sxs-lookup"><span data-stu-id="5048e-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="5048e-143">Следующий пример Hello создает TCP-зонды.</span><span class="sxs-lookup"><span data-stu-id="5048e-143">hello following example creates a TCP probe.</span></span> <span data-ttu-id="5048e-144">Вы также можете создать настраиваемую пробу HTTP для более детальных проверок.</span><span class="sxs-lookup"><span data-stu-id="5048e-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="5048e-145">При использовании пользовательских проверку HTTP, необходимо создать страницу проверки работоспособности hello, таких как *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="5048e-145">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="5048e-146">Hello пробы должен возвращать **HTTP 200 OK** ответа для узла hello tookeep подсистемы балансировки нагрузки hello в поворота.</span><span class="sxs-lookup"><span data-stu-id="5048e-146">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="5048e-147">использовать toocreate TCP-зонды работоспособности [зонд балансировки нагрузки сети az создать](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="5048e-147">toocreate a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="5048e-148">Hello следующий пример создает зонда работоспособности с именем *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="5048e-148">hello following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="5048e-149">Создание правила балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="5048e-149">Create a load balancer rule</span></span>
<span data-ttu-id="5048e-150">Правило подсистемы балансировки нагрузки — toodefine используется как трафика является распределенной toohello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5048e-150">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="5048e-151">Можно определить hello интерфейсный IP-конфигурацию для hello входящий трафик и hello серверной части IP пула tooreceive hello трафика, а также требуемых исходных hello и порт назначения.</span><span class="sxs-lookup"><span data-stu-id="5048e-151">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="5048e-152">toomake убедиться, что только работоспособное ВМ получать трафик также определять toouse проверки работоспособности hello.</span><span class="sxs-lookup"><span data-stu-id="5048e-152">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="5048e-153">Создайте правило балансировщика нагрузки с помощью команды [az network lb rule create](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="5048e-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="5048e-154">Hello следующий код создает правило с именем *myLoadBalancerRule*, использует hello *myHealthProbe* проверки работоспособности и сальдо трафик через порт *80*:</span><span class="sxs-lookup"><span data-stu-id="5048e-154">hello following example creates a rule named *myLoadBalancerRule*, uses hello *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

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


## <a name="configure-virtual-network"></a><span data-ttu-id="5048e-155">Настройка виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="5048e-155">Configure virtual network</span></span>
<span data-ttu-id="5048e-156">Перед развертыванием некоторые виртуальные машины и можно проверить балансировки, создайте hello, поддерживающие ресурсы виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="5048e-156">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="5048e-157">Дополнительные сведения о виртуальных сетях см. в разделе hello [управление виртуальными сетями Azure](tutorial-virtual-network.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="5048e-157">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="5048e-158">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="5048e-158">Create network resources</span></span>
<span data-ttu-id="5048e-159">Создайте виртуальную сеть с помощью команды [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="5048e-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="5048e-160">Hello следующий пример создает виртуальную сеть с именем *myVnet* с подсеть с именем *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="5048e-160">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="5048e-161">использовать tooadd группы безопасности сети, [создать az сети nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="5048e-161">tooadd a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="5048e-162">Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="5048e-162">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="5048e-163">Создайте правило группы безопасности сети с помощью команды [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="5048e-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="5048e-164">Hello следующий пример создает правило группы сетевой безопасности с именем *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="5048e-164">hello following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="5048e-165">Для создания виртуальных сетевых карт используется команда [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="5048e-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="5048e-166">Hello следующий пример создает три виртуальных сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="5048e-166">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="5048e-167">(Один виртуальный сетевой Адаптер для каждой виртуальной Машины, создать приложение hello следующих шагов).</span><span class="sxs-lookup"><span data-stu-id="5048e-167">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="5048e-168">Можно создать в любое время дополнительных виртуальных сетевых адаптеров и виртуальные машины и добавить их toohello балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="5048e-168">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="5048e-169">Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="5048e-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="5048e-170">Создание конфигурации cloud-init</span><span class="sxs-lookup"><span data-stu-id="5048e-170">Create cloud-init config</span></span>
<span data-ttu-id="5048e-171">В предыдущем учебнике на [как toocustomize виртуальной машины Linux при первой загрузке](tutorial-automate-vm-deployment.md), вы узнали, каким образом tooautomate настройки виртуальной Машины с инициализацией облака.</span><span class="sxs-lookup"><span data-stu-id="5048e-171">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="5048e-172">Можно использовать hello же tooinstall файл конфигурации облачной init NGINX и выполнение простого приложения Node.js «Hello World».</span><span class="sxs-lookup"><span data-stu-id="5048e-172">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="5048e-173">В вашей текущей оболочке, создайте файл с именем *init.txt облака* и вставить hello следующая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="5048e-173">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="5048e-174">Например можно создайте файл hello в hello облака оболочки не на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="5048e-174">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="5048e-175">Введите `sensible-editor cloud-init.txt` toocreate hello файла и просмотреть список доступных редакторов.</span><span class="sxs-lookup"><span data-stu-id="5048e-175">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="5048e-176">Убедитесь, что этот файл всей облачной init hello скопирован верно, особенно hello первой строки:</span><span class="sxs-lookup"><span data-stu-id="5048e-176">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

### <a name="create-virtual-machines"></a><span data-ttu-id="5048e-177">Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="5048e-177">Create virtual machines</span></span>
<span data-ttu-id="5048e-178">tooimprove hello высокий уровень доступности приложения, поместите виртуальные машины в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="5048e-178">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="5048e-179">Дополнительные сведения о группах доступности см. в разделе hello предыдущих [как виртуальные машины высокой надежности toocreate](tutorial-availability-sets.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="5048e-179">For more information about availability sets, see hello previous [How toocreate highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="5048e-180">Создайте группу доступности с помощью команды [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="5048e-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="5048e-181">Hello следующий пример создает именованный набор доступности *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="5048e-181">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="5048e-182">Теперь можно создавать виртуальные машины hello с [создания виртуальной машины az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="5048e-182">Now you can create hello VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="5048e-183">Hello следующий пример создает три виртуальные машины и создает ключи SSH, если они еще не существует:</span><span class="sxs-lookup"><span data-stu-id="5048e-183">hello following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

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

<span data-ttu-id="5048e-184">Существует фоновых задач, продолжить toorun после hello Azure CLI возвращает toohello строки.</span><span class="sxs-lookup"><span data-stu-id="5048e-184">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="5048e-185">Hello `--no-wait` параметра не ожидать все hello toocomplete задачи.</span><span class="sxs-lookup"><span data-stu-id="5048e-185">hello `--no-wait` parameter does not wait for all hello tasks toocomplete.</span></span> <span data-ttu-id="5048e-186">Он может быть другой несколько минут, чтобы получить доступ к приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5048e-186">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="5048e-187">Hello зонда работоспособности подсистемы балансировки нагрузки автоматически определяет, когда приложение hello выполняется на каждой виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="5048e-187">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="5048e-188">После запуска приложение hello правило подсистемы балансировки нагрузки hello запускает toodistribute трафика.</span><span class="sxs-lookup"><span data-stu-id="5048e-188">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="5048e-189">Проверка балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="5048e-189">Test load balancer</span></span>
<span data-ttu-id="5048e-190">Получить hello общедоступный IP-адрес балансировки нагрузки, с [az сети public-ip show](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="5048e-190">Obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="5048e-191">Hello следующий пример извлекает hello IP-адрес для *myPublicIP* созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="5048e-191">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="5048e-192">После этого можно вводить hello общедоступный IP-адрес в tooa веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="5048e-192">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="5048e-193">Запомнить - занимает несколько минут hello hello виртуальные машины toobe готовности начала toothem toodistribute трафика подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="5048e-193">Remember - it takes a few minutes hello hello VMs toobe ready before hello load balancer starts toodistribute traffic toothem.</span></span> <span data-ttu-id="5048e-194">Откроется приложение Hello, включая имя узла виртуальной Машины hello hello балансировки нагрузки, hello распределенных tooas трафика в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="5048e-194">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Запуск приложения Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="5048e-196">Подсистема балансировки нагрузки hello toosee распределять трафик между все три виртуальные машины, запускающий ваше приложение, вы может принудительно обновить веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="5048e-196">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="5048e-197">Добавление и удаление виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="5048e-197">Add and remove VMs</span></span>
<span data-ttu-id="5048e-198">Может потребоваться tooperform обслуживания на hello приложения, таких как установка обновления ОС работающих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5048e-198">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="5048e-199">toodeal с приложением tooyour большего объема трафика, может потребоваться tooadd дополнительных ВМ.</span><span class="sxs-lookup"><span data-stu-id="5048e-199">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="5048e-200">В этом разделе показано, как tooremove или добавить виртуальную Машину из балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="5048e-200">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="5048e-201">Удалите виртуальную Машину из балансировки нагрузки hello</span><span class="sxs-lookup"><span data-stu-id="5048e-201">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="5048e-202">Можно удалить виртуальную Машину из hello серверный пул адресов с [удалить az сетевых ip конфигурация пул сетевых адресов-](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="5048e-202">You can remove a VM from hello backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="5048e-203">Следующий пример удаляет Hello hello виртуальный сетевой Адаптер для **myVM2** из *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="5048e-203">hello following example removes hello virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="5048e-204">подсистемы балансировки нагрузки hello toosee распределять трафик между hello остальные две виртуальные машины под управлением приложения вы можно принудительно обновить веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="5048e-204">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="5048e-205">Теперь можно выполнить обслуживание на hello виртуальной Машины, таких как установка обновлений операционной системы или перезагрузки виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5048e-205">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="5048e-206">Добавляет подсистему балансировки нагрузки виртуальной Машины toohello</span><span class="sxs-lookup"><span data-stu-id="5048e-206">Add a VM toohello load balancer</span></span>
<span data-ttu-id="5048e-207">После выполнения обслуживания виртуальной Машины, или если требуется емкость tooexpand, можно добавить пул адресов серверной части ВМ toohello с [az сетевых ip конфигурация пул сетевых адресов-добавить](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="5048e-207">After performing VM maintenance, or if you need tooexpand capacity, you can add a VM toohello backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="5048e-208">Hello следующий пример добавляет hello виртуальный сетевой Адаптер для **myVM2** слишком*myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="5048e-208">hello following example adds hello virtual NIC for **myVM2** too*myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="5048e-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5048e-209">Next steps</span></span>
<span data-ttu-id="5048e-210">В этом учебнике вы создается подсистемы балансировки нагрузки и прикрепляется tooit виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5048e-210">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="5048e-211">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="5048e-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5048e-212">Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5048e-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="5048e-213">Создание пробы работоспособности балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="5048e-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="5048e-214">создавать правила трафика подсистемы балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="5048e-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="5048e-215">Использование облака init toocreate простое приложение Node.js</span><span class="sxs-lookup"><span data-stu-id="5048e-215">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="5048e-216">Создание виртуальных машин и присоединения tooa балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="5048e-216">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="5048e-217">Просмотр балансировщика нагрузки в действии</span><span class="sxs-lookup"><span data-stu-id="5048e-217">View a load balancer in action</span></span>
> * <span data-ttu-id="5048e-218">добавлять и удалять виртуальные машины из подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5048e-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="5048e-219">Дополнительные сведения о виртуальной сети Azure компоненты приращения Далее учебника toolearn toohello.</span><span class="sxs-lookup"><span data-stu-id="5048e-219">Advance toohello next tutorial toolearn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5048e-220">Управление виртуальными сетями Azure и виртуальными машинами Linux с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5048e-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
