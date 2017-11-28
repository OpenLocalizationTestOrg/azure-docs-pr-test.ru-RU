---
title: "Виртуальные сети Azure и виртуальные машины Linux | Документы Майкрософт"
description: "Руководство по управлению виртуальными сетями Azure и виртуальными машинами Linux с помощью Azure CLI"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2366905b8160675f77cbc41ba97540af70be8c01
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-the-azure-cli"></a><span data-ttu-id="305a9-103">Управление виртуальными сетями Azure и виртуальными машинами Linux с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="305a9-103">Manage Azure Virtual Networks and Linux Virtual Machines with the Azure CLI</span></span>

<span data-ttu-id="305a9-104">Виртуальные машины Azure осуществляют внутреннее и внешнее взаимодействие через сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="305a9-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="305a9-105">В этом руководстве содержатся сведения о развертывании двух виртуальных машин и настройке для них сети Azure.</span><span class="sxs-lookup"><span data-stu-id="305a9-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="305a9-106">Примеры, описанные в этом руководстве, предполагают, что на виртуальных машинах размещается веб-приложение с сервером базы данных, но здесь не описывается развертывание самого приложения.</span><span class="sxs-lookup"><span data-stu-id="305a9-106">The examples in this tutorial assume that the VMs are hosting a web application with a database back-end, however an application is not deployed in the tutorial.</span></span> <span data-ttu-id="305a9-107">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="305a9-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="305a9-108">развернуть виртуальную сеть;</span><span class="sxs-lookup"><span data-stu-id="305a9-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="305a9-109">создавать подсеть в виртуальной сети;</span><span class="sxs-lookup"><span data-stu-id="305a9-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="305a9-110">присоединять виртуальную машину к подсети;</span><span class="sxs-lookup"><span data-stu-id="305a9-110">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="305a9-111">управлять общедоступными IP-адресами виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="305a9-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="305a9-112">защищать входящий интернет-трафик;</span><span class="sxs-lookup"><span data-stu-id="305a9-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="305a9-113">защищать трафик между виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="305a9-113">Secure VM to VM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="305a9-114">Если вы решили установить и использовать интерфейс командной строки локально, то для работы с этим руководством вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="305a9-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="305a9-115">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="305a9-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="305a9-116">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="305a9-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="305a9-117">Обзор сети виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="305a9-117">VM networking overview</span></span>

<span data-ttu-id="305a9-118">Виртуальные сети Azure позволяют устанавливать безопасные сетевые подключения между виртуальными машинами, в Интернете, а также между другими службами Azure, такими как база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="305a9-118">Azure virtual networks enable secure network connections between virtual machines, the internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="305a9-119">Виртуальные сети разбиты на логические сегменты — подсети.</span><span class="sxs-lookup"><span data-stu-id="305a9-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="305a9-120">Подсети позволяют контролировать поток сетевого трафика. Это своего рода периметр безопасности.</span><span class="sxs-lookup"><span data-stu-id="305a9-120">Subnets are used to control network flow, and as a security boundary.</span></span> <span data-ttu-id="305a9-121">При развертывании виртуальная машина обычно содержит виртуальный сетевой интерфейс, подключенный к подсети.</span><span class="sxs-lookup"><span data-stu-id="305a9-121">When deploying a VM, it generally includes a virtual network interface, which is attached to a subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="305a9-122">Развертывание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="305a9-122">Deploy virtual network</span></span>

<span data-ttu-id="305a9-123">В этом руководстве создается виртуальная сеть с двумя подсетями:</span><span class="sxs-lookup"><span data-stu-id="305a9-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="305a9-124">интерфейсная подсеть для размещения веб-приложения и внутренняя подсеть для размещения сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="305a9-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="305a9-125">Прежде чем создать виртуальную сеть, выполните команду [az group create](/cli/azure/group#create), чтобы создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="305a9-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="305a9-126">Следующий пример позволяет создать группу ресурсов *myRGNetwork* в расположении eastus.</span><span class="sxs-lookup"><span data-stu-id="305a9-126">The following example creates a resource group named *myRGNetwork* in the eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="305a9-127">Создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="305a9-127">Create virtual network</span></span>

<span data-ttu-id="305a9-128">Создайте виртуальную сеть с помощью команды [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="305a9-128">Us the [az network vnet create](/cli/azure/network/vnet#create) command to create a virtual network.</span></span> <span data-ttu-id="305a9-129">В этом примере создается сеть *mvVnet* с префиксом адреса *10.0.0.0/16*,</span><span class="sxs-lookup"><span data-stu-id="305a9-129">In this example, the network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="305a9-130">а также подсеть *mySubnetFrontEnd* с префиксом *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="305a9-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="305a9-131">Далее в этом руководстве мы подключим интерфейсную виртуальную машину к этой подсети.</span><span class="sxs-lookup"><span data-stu-id="305a9-131">Later in this tutorial a front-end VM is connected to this subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="305a9-132">Создание подсети</span><span class="sxs-lookup"><span data-stu-id="305a9-132">Create subnet</span></span>

<span data-ttu-id="305a9-133">Добавьте новую подсеть к виртуальной сети с помощью команды [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="305a9-133">A new subnet is added to the virtual network using the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="305a9-134">В этом примере создается подсеть *mySubnetBackEnd* с префиксом адреса *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="305a9-134">In this example, the subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="305a9-135">Она используется со всеми внутренними службами.</span><span class="sxs-lookup"><span data-stu-id="305a9-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="305a9-136">На этом этапе мы создали сеть и разбили ее на две подсети — одна для интерфейсных служб, а вторая для внутренних служб.</span><span class="sxs-lookup"><span data-stu-id="305a9-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="305a9-137">В следующем разделе мы создадим виртуальные машины и подключим их к этим подсетям.</span><span class="sxs-lookup"><span data-stu-id="305a9-137">In the next section, virtual machines are created and connected to these subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="305a9-138">Общие сведения об общедоступном IP-адресе</span><span class="sxs-lookup"><span data-stu-id="305a9-138">Understand public IP address</span></span>

<span data-ttu-id="305a9-139">Общедоступный IP-адрес обеспечивает доступность ресурсов Azure в Интернете.</span><span class="sxs-lookup"><span data-stu-id="305a9-139">A public IP address allows Azure resources to be accessible on the internet.</span></span> <span data-ttu-id="305a9-140">В этом разделе руководства рассматривается настройка общедоступного IP-адреса для созданной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="305a9-140">In this section of the tutorial, a VM is created to demonstrate how to work with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="305a9-141">Способ выделения</span><span class="sxs-lookup"><span data-stu-id="305a9-141">Allocation method</span></span>

<span data-ttu-id="305a9-142">Общедоступный IP-адрес может быть динамическим или статическим.</span><span class="sxs-lookup"><span data-stu-id="305a9-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="305a9-143">По умолчанию выделяется динамический общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="305a9-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="305a9-144">После освобождения виртуальной машины освобождаются также и динамические IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="305a9-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="305a9-145">Таким образом, IP-адреса изменяются во время каждой операции с освобождением виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="305a9-145">This behavior causes the IP address to change during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="305a9-146">При использовании статического метода выделения IP-адрес остается назначенным виртуальной машине, даже если она в освобожденном состоянии.</span><span class="sxs-lookup"><span data-stu-id="305a9-146">The allocation method can be set to static, which ensures that the IP address remain assigned to a VM, even during a deallocated state.</span></span> <span data-ttu-id="305a9-147">В этом случае вы не сможете указать IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="305a9-147">When using a statically allocated IP address, the IP address itself cannot be specified.</span></span> <span data-ttu-id="305a9-148">Он выделяется из пула доступных адресов.</span><span class="sxs-lookup"><span data-stu-id="305a9-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="305a9-149">Динамическое выделение</span><span class="sxs-lookup"><span data-stu-id="305a9-149">Dynamic allocation</span></span>

<span data-ttu-id="305a9-150">При создании виртуальной машины с помощью команды [az vm create](/cli/azure/vm#create) по умолчанию выделяется динамический общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="305a9-150">When creating a VM with the [az vm create](/cli/azure/vm#create) command, the default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="305a9-151">Следующий пример позволяет создать виртуальную машину с динамическим IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="305a9-151">In the following example, a VM is created with a dynamic IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a><span data-ttu-id="305a9-152">Статическое выделение</span><span class="sxs-lookup"><span data-stu-id="305a9-152">Static allocation</span></span>

<span data-ttu-id="305a9-153">При создании виртуальной машины с помощью команды [az vm create](/cli/azure/vm#create) добавьте аргумент `--public-ip-address-allocation static`, чтобы назначить статический общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="305a9-153">When creating a virtual machine using the [az vm create](/cli/azure/vm#create) command, include the `--public-ip-address-allocation static` argument to assign a static public IP address.</span></span> <span data-ttu-id="305a9-154">Эта операция не описана в этом руководстве, но в следующем разделе показано, как изменить динамический IP-адрес на статический.</span><span class="sxs-lookup"><span data-stu-id="305a9-154">This operation is not demonstrated in this tutorial, however in the next section a dynamically allocated IP address is changed to a statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="305a9-155">Изменение метода выделения</span><span class="sxs-lookup"><span data-stu-id="305a9-155">Change allocation method</span></span>

<span data-ttu-id="305a9-156">Метод выделения IP-адресов можно изменить с помощью команды [az network public-ip update](/cli/azure/network/public-ip#update).</span><span class="sxs-lookup"><span data-stu-id="305a9-156">The IP address allocation method can be changed using the [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="305a9-157">В этом примере метод выделения IP-адреса интерфейсной виртуальной машины изменяется на статический.</span><span class="sxs-lookup"><span data-stu-id="305a9-157">In this example, the IP address allocation method of the front-end VM is changed to static.</span></span>

<span data-ttu-id="305a9-158">Сначала отмените подготовку виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="305a9-158">First, deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="305a9-159">Обновите метод выделения, используя команду [az network public-ip update](/cli/azure/network/public-ip#update).</span><span class="sxs-lookup"><span data-stu-id="305a9-159">Use the [az network public-ip update](/cli/azure/network/public-ip#update) command to update the allocation method.</span></span> <span data-ttu-id="305a9-160">В этом случае для параметра `--allocation-method` необходимо задать значение *static*.</span><span class="sxs-lookup"><span data-stu-id="305a9-160">In this case, the `--allocation-method` is being set to *static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="305a9-161">Запустите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="305a9-161">Start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="305a9-162">Создание виртуальной машины без общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="305a9-162">No public IP address</span></span>

<span data-ttu-id="305a9-163">Во многих случаях виртуальная машина не должна быть доступна через Интернет.</span><span class="sxs-lookup"><span data-stu-id="305a9-163">Often, a VM does not need to be accessible over the internet.</span></span> <span data-ttu-id="305a9-164">Чтобы создать виртуальную машину без общедоступного IP-адреса, используйте аргумент `--public-ip-address ""` с пустыми двойными кавычками.</span><span class="sxs-lookup"><span data-stu-id="305a9-164">To create a VM without a public IP address, use the `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="305a9-165">Эта конфигурация рассматривается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="305a9-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="305a9-166">защищают сетевой трафик;</span><span class="sxs-lookup"><span data-stu-id="305a9-166">Secure network traffic</span></span>

<span data-ttu-id="305a9-167">Группа безопасности сети (NSG) содержит перечень правил безопасности, которые разрешают или запрещают передачу сетевого трафика к ресурсам, подключенным к виртуальным сетям Azure.</span><span class="sxs-lookup"><span data-stu-id="305a9-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to Azure Virtual Networks (VNet).</span></span> <span data-ttu-id="305a9-168">Группы безопасности сети (NSG) можно связать с подсетями или отдельными сетевыми интерфейсами.</span><span class="sxs-lookup"><span data-stu-id="305a9-168">NSGs can be associated to subnets or individual network interfaces.</span></span> <span data-ttu-id="305a9-169">Группа безопасности сети, связанная с сетевым интерфейсом, применяется только к связанной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="305a9-169">When an NSG is associated with a network interface, it applies only the associated VM.</span></span> <span data-ttu-id="305a9-170">Если группа безопасности сети связана с подсетью, эти правила применяются ко всем ресурсам в подсети.</span><span class="sxs-lookup"><span data-stu-id="305a9-170">When an NSG is associated to a subnet, the rules apply to all resources connected to the subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="305a9-171">Правила группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="305a9-171">Network security group rules</span></span>

<span data-ttu-id="305a9-172">Правила группы безопасности сети определяют сетевые порты, через которые разрешен или запрещен трафик.</span><span class="sxs-lookup"><span data-stu-id="305a9-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="305a9-173">Эти правила также могут включать исходные и целевые диапазоны IP-адресов, что позволяет контролировать трафик между определенными системами и подсетями.</span><span class="sxs-lookup"><span data-stu-id="305a9-173">The rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="305a9-174">Правилам также присваивается приоритет (от 1 до 4096),</span><span class="sxs-lookup"><span data-stu-id="305a9-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="305a9-175">и они оцениваются в порядке приоритета.</span><span class="sxs-lookup"><span data-stu-id="305a9-175">Rules are evaluated in the order of priority.</span></span> <span data-ttu-id="305a9-176">Правило с приоритетом 100 оценивается перед правилом с приоритетом 200.</span><span class="sxs-lookup"><span data-stu-id="305a9-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="305a9-177">Все группы NSG содержат набор правил по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="305a9-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="305a9-178">Эти правила нельзя удалить, но у них самый низкий приоритет, поэтому их можно переопределить, создав другие правила.</span><span class="sxs-lookup"><span data-stu-id="305a9-178">The default rules cannot be deleted, but because they are assigned the lowest priority, they can be overridden by the rules that you create.</span></span>

- <span data-ttu-id="305a9-179">**Виртуальная сеть.** Входящий и исходящий трафик виртуальной сети разрешен в обоих направлениях.</span><span class="sxs-lookup"><span data-stu-id="305a9-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="305a9-180">**Интернет.** Исходящий трафик разрешен, но входящий трафик заблокирован.</span><span class="sxs-lookup"><span data-stu-id="305a9-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="305a9-181">**Подсистема балансировки нагрузки.** Разрешает Azure Load Balancer инициировать проверку работоспособности виртуальных машин и экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="305a9-181">**Load balancer** - Allow Azure’s load balancer to probe the health of your VMs and role instances.</span></span> <span data-ttu-id="305a9-182">Если набор балансировки нагрузки не используется, это правило можно переопределить.</span><span class="sxs-lookup"><span data-stu-id="305a9-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="305a9-183">Создание групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="305a9-183">Create network security groups</span></span>

<span data-ttu-id="305a9-184">Группу безопасности сети можно создать вместе с виртуальной машиной, используя команду [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="305a9-184">A network security group can be created at the same time as a VM using the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="305a9-185">В этом случае группа безопасности сети связывается с сетевым интерфейсом виртуальных машин и автоматически создается правило NSG, разрешающее прохождение трафика через порт *22* из любого источника.</span><span class="sxs-lookup"><span data-stu-id="305a9-185">When doing so, the NSG is associated with the VMs network interface and an NSG rule is auto created to allow traffic on port *22* from any source.</span></span> <span data-ttu-id="305a9-186">Ранее в этом руководстве мы создали интерфейсную виртуальную машину, вместе с которой была автоматически создана группа безопасности сети переднего плана.</span><span class="sxs-lookup"><span data-stu-id="305a9-186">Earlier in this tutorial, the front-end NSG was auto-created with the front-end VM.</span></span> <span data-ttu-id="305a9-187">Кроме того, было также создано правило NSG для порта 22.</span><span class="sxs-lookup"><span data-stu-id="305a9-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="305a9-188">В некоторых случаях есть смысл заранее создать группу безопасности сети, например, если не нужно создавать правила SSH по умолчанию или если группу безопасности сети нужно присоединить к подсети.</span><span class="sxs-lookup"><span data-stu-id="305a9-188">In some cases, it may be helpful to pre-create an NSG, such as when default SSH rules should not be created, or when the NSG should be attached to a subnet.</span></span> 

<span data-ttu-id="305a9-189">Создайте группу безопасности сети с помощью команды [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="305a9-189">Use the [az network nsg create](/cli/azure/network/nsg#create) command to create a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="305a9-190">В этом случае группа безопасности сети будет связана с подсетью, а не сетевым интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="305a9-190">Instead of associating the NSG to a network interface, it is associated with a subnet.</span></span> <span data-ttu-id="305a9-191">В этой конфигурации все виртуальные машины, подключенные к подсети, наследуют правила NSG.</span><span class="sxs-lookup"><span data-stu-id="305a9-191">In this configuration, any VM that is attached to the subnet inherits the NSG rules.</span></span>

<span data-ttu-id="305a9-192">Обновите имеющуюся подсеть *mySubnetBackEnd*, включив в нее новую группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="305a9-192">Update the existing subnet named *mySubnetBackEnd* with the new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="305a9-193">Теперь создайте виртуальную машину и присоедините ее к подсети *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="305a9-193">Now create a virtual machine, which is attached to the *mySubnetBackEnd*.</span></span> <span data-ttu-id="305a9-194">Обратите внимание, что в качестве значения аргумента `--nsg` используются пустые двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="305a9-194">Notice that the `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="305a9-195">Вместе с виртуальной машиной не нужно создавать группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="305a9-195">An NSG does not need to be created with the VM.</span></span> <span data-ttu-id="305a9-196">Виртуальная машина будет подключена к внутренней подсети, которая защищена с помощью предварительно созданной внутренней группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="305a9-196">The VM is attached to the back-end subnet, which is protected with the pre-created back-end NSG.</span></span> <span data-ttu-id="305a9-197">Эта группа безопасности сети применяется к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="305a9-197">This NSG applies to the VM.</span></span> <span data-ttu-id="305a9-198">Кроме того, обратите внимание, что в качестве значения аргумента `--public-ip-address` используются пустые двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="305a9-198">Also, notice here that the `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="305a9-199">Эта конфигурация создает виртуальную машину без общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="305a9-199">This configuration creates a VM without a public IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a><span data-ttu-id="305a9-200">Защита входящего трафика</span><span class="sxs-lookup"><span data-stu-id="305a9-200">Secure incoming traffic</span></span>

<span data-ttu-id="305a9-201">При создании интерфейсной виртуальной машины также было создано правило NSG, разрешающее входящий трафик через порт 22.</span><span class="sxs-lookup"><span data-stu-id="305a9-201">When the front-end VM was created, an NSG rule was created to allow incoming traffic on port 22.</span></span> <span data-ttu-id="305a9-202">Это правило разрешает SSH-подключения к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="305a9-202">This rule allows SSH connections to the VM.</span></span> <span data-ttu-id="305a9-203">В этом примере трафик также необходимо разрешить через порт *80*.</span><span class="sxs-lookup"><span data-stu-id="305a9-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="305a9-204">Такая конфигурация обеспечивает доступ к веб-приложению на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="305a9-204">This configuration allows a web application to be accessed on the VM.</span></span>

<span data-ttu-id="305a9-205">Создайте правило для порта *80* с помощью команды [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="305a9-205">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port *80*.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

<span data-ttu-id="305a9-206">Теперь интерфейсная виртуальная машина доступна только через порты *22* и *80*.</span><span class="sxs-lookup"><span data-stu-id="305a9-206">The front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="305a9-207">Весь остальной входящий трафик блокируется группой безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="305a9-207">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="305a9-208">Иногда есть смысл визуализировать конфигурации правил NSG.</span><span class="sxs-lookup"><span data-stu-id="305a9-208">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="305a9-209">Получите конфигурацию правила NSG с помощью команды [az network rule list](/cli/azure/network/nsg/rule#list).</span><span class="sxs-lookup"><span data-stu-id="305a9-209">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="305a9-210">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="305a9-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-to-vm-traffic"></a><span data-ttu-id="305a9-211">Защита трафика между виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="305a9-211">Secure VM to VM traffic</span></span>

<span data-ttu-id="305a9-212">Правила группы безопасности сети также можно применить между виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="305a9-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="305a9-213">В этом примере интерфейсная виртуальная машина должна взаимодействовать с внутренней виртуальной машиной через порт *22* и *3306*.</span><span class="sxs-lookup"><span data-stu-id="305a9-213">For this example, the front-end VM needs to communicate with the back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="305a9-214">Эта конфигурация разрешает SSH-подключения из интерфейсной виртуальной машины, а также разрешает приложению, расположенному на этой виртуальной машине, взаимодействовать с внутренней базой данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="305a9-214">This configuration allows SSH connections from the front-end VM, and also allow an application on the front-end VM to communicate with a back-end MySQL database.</span></span> <span data-ttu-id="305a9-215">Весь остальной трафик между интерфейсной и внутренней виртуальными машинами должен блокироваться.</span><span class="sxs-lookup"><span data-stu-id="305a9-215">All other traffic should be blocked between the front-end and back-end virtual machines.</span></span>

<span data-ttu-id="305a9-216">Создайте правило для порта 22 с помощью команды [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="305a9-216">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port 22.</span></span> <span data-ttu-id="305a9-217">Обратите внимание, что аргумент `--source-address-prefix` имеет значение *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="305a9-217">Notice that the `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="305a9-218">Такая конфигурация гарантирует, что только трафик из интерфейсной подсети сможет пройти через группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="305a9-218">This configuration ensures that only traffic from the front-end subnet is allowed through the NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

<span data-ttu-id="305a9-219">Теперь добавьте правило, разрешающее трафик MySQL через порт 3306.</span><span class="sxs-lookup"><span data-stu-id="305a9-219">Now add a rule for MySQL traffic on port 3306.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

<span data-ttu-id="305a9-220">И наконец, так как группы безопасности сети имеют правила по умолчанию, разрешающие весь трафик между виртуальными машинами в той же виртуальной сети, вы можете создать правило блокировки всего трафика во внутренних группах безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="305a9-220">Finally, because NSGs have a default rule allowing all traffic between VMs in the same VNet, a rule can be created for the back-end NSGs to block all traffic.</span></span> <span data-ttu-id="305a9-221">Обратите внимание, что аргумент `--priority` имеет значение *300*, что меньше значения приоритета правил NSG и MySQL.</span><span class="sxs-lookup"><span data-stu-id="305a9-221">Notice here that the `--priority` is given a value of *300*, which is lower that both the NSG and MySQL rules.</span></span> <span data-ttu-id="305a9-222">Такая конфигурация гарантирует, что трафик SSH и MySQL по-прежнему сможет проходить через группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="305a9-222">This configuration ensures that SSH and MySQL traffic is still allowed through the NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

<span data-ttu-id="305a9-223">Теперь внутренняя виртуальная машина доступна только через порты *22* и *3306* из интерфейсной подсети.</span><span class="sxs-lookup"><span data-stu-id="305a9-223">The back-end VM is now only accessible on port *22* and port *3306* from the front-end subnet.</span></span> <span data-ttu-id="305a9-224">Весь остальной входящий трафик блокируется группой безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="305a9-224">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="305a9-225">Иногда есть смысл визуализировать конфигурации правил NSG.</span><span class="sxs-lookup"><span data-stu-id="305a9-225">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="305a9-226">Получите конфигурацию правила NSG с помощью команды [az network rule list](/cli/azure/network/nsg/rule#list).</span><span class="sxs-lookup"><span data-stu-id="305a9-226">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="305a9-227">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="305a9-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="305a9-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="305a9-228">Next steps</span></span>

<span data-ttu-id="305a9-229">В этом руководстве вы создали и защитили сети Azure с точки зрения виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="305a9-229">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> <span data-ttu-id="305a9-230">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="305a9-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="305a9-231">развертывать виртуальную сеть;</span><span class="sxs-lookup"><span data-stu-id="305a9-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="305a9-232">создавать подсеть в виртуальной сети;</span><span class="sxs-lookup"><span data-stu-id="305a9-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="305a9-233">присоединять виртуальную машину к подсети;</span><span class="sxs-lookup"><span data-stu-id="305a9-233">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="305a9-234">управлять общедоступными IP-адресами виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="305a9-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="305a9-235">защищать входящий интернет-трафик;</span><span class="sxs-lookup"><span data-stu-id="305a9-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="305a9-236">защищать трафик между виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="305a9-236">Secure VM to VM traffic</span></span>

<span data-ttu-id="305a9-237">Перейдите к следующему руководству, чтобы узнать о защите данных на виртуальных машинах с помощью службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="305a9-237">Advance to the next tutorial to learn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="305a9-238">Архивация виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="305a9-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
