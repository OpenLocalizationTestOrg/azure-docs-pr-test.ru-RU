---
title: "aaaAzure виртуальных сетей и виртуальных машин Linux | Документы Microsoft"
description: "Учебник - управление виртуальными сетями Azure и виртуальных машин Linux с hello Azure CLI"
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
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a><span data-ttu-id="75a0b-103">Управление виртуальными сетями Azure и виртуальных машин Linux с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="75a0b-103">Manage Azure Virtual Networks and Linux Virtual Machines with hello Azure CLI</span></span>

<span data-ttu-id="75a0b-104">Виртуальные машины Azure осуществляют внутреннее и внешнее взаимодействие через сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="75a0b-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="75a0b-105">В этом руководстве содержатся сведения о развертывании двух виртуальных машин и настройке для них сети Azure.</span><span class="sxs-lookup"><span data-stu-id="75a0b-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="75a0b-106">Hello в примерах этого учебника предполагается, что виртуальные машины hello размещается веб-приложение с базы данных серверной части, однако приложение не развертывается в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-106">hello examples in this tutorial assume that hello VMs are hosting a web application with a database back-end, however an application is not deployed in hello tutorial.</span></span> <span data-ttu-id="75a0b-107">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="75a0b-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75a0b-108">развернуть виртуальную сеть;</span><span class="sxs-lookup"><span data-stu-id="75a0b-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="75a0b-109">создавать подсеть в виртуальной сети;</span><span class="sxs-lookup"><span data-stu-id="75a0b-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="75a0b-110">Подключите виртуальные машины tooa подсети</span><span class="sxs-lookup"><span data-stu-id="75a0b-110">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="75a0b-111">управлять общедоступными IP-адресами виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="75a0b-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="75a0b-112">защищать входящий интернет-трафик;</span><span class="sxs-lookup"><span data-stu-id="75a0b-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="75a0b-113">Защита виртуальной Машины tooVM трафика</span><span class="sxs-lookup"><span data-stu-id="75a0b-113">Secure VM tooVM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="75a0b-114">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="75a0b-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="75a0b-115">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="75a0b-116">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="75a0b-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="75a0b-117">Обзор сети виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="75a0b-117">VM networking overview</span></span>

<span data-ttu-id="75a0b-118">Виртуальные сети Azure включить безопасные сетевые подключения между виртуальными машинами, hello Интернета и других служб Azure, таких как базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="75a0b-118">Azure virtual networks enable secure network connections between virtual machines, hello internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="75a0b-119">Виртуальные сети разбиты на логические сегменты — подсети.</span><span class="sxs-lookup"><span data-stu-id="75a0b-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="75a0b-120">Используются подсети toocontrol сетевой поток и в качестве границы безопасности.</span><span class="sxs-lookup"><span data-stu-id="75a0b-120">Subnets are used toocontrol network flow, and as a security boundary.</span></span> <span data-ttu-id="75a0b-121">При развертывании виртуальной Машины, обычно содержат виртуального сетевого интерфейса, подключенных tooa подсеть.</span><span class="sxs-lookup"><span data-stu-id="75a0b-121">When deploying a VM, it generally includes a virtual network interface, which is attached tooa subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="75a0b-122">Развертывание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="75a0b-122">Deploy virtual network</span></span>

<span data-ttu-id="75a0b-123">В этом руководстве создается виртуальная сеть с двумя подсетями:</span><span class="sxs-lookup"><span data-stu-id="75a0b-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="75a0b-124">интерфейсная подсеть для размещения веб-приложения и внутренняя подсеть для размещения сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="75a0b-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="75a0b-125">Прежде чем создать виртуальную сеть, выполните команду [az group create](/cli/azure/group#create), чтобы создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="75a0b-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="75a0b-126">Hello следующий пример создает группу ресурсов с именем *myRGNetwork* в расположении eastus hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-126">hello following example creates a resource group named *myRGNetwork* in hello eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="75a0b-127">Создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="75a0b-127">Create virtual network</span></span>

<span data-ttu-id="75a0b-128">Здравствуйте, нам [создания az сети vnet](/cli/azure/network/vnet#create) toocreate команда виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="75a0b-128">Us hello [az network vnet create](/cli/azure/network/vnet#create) command toocreate a virtual network.</span></span> <span data-ttu-id="75a0b-129">В этом примере hello сети называется *mvVnet* и задан префикс адреса *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="75a0b-129">In this example, hello network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="75a0b-130">а также подсеть *mySubnetFrontEnd* с префиксом *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="75a0b-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="75a0b-131">Далее в этом учебнике переднего плана виртуальная машина является подключенных toothis подсети.</span><span class="sxs-lookup"><span data-stu-id="75a0b-131">Later in this tutorial a front-end VM is connected toothis subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="75a0b-132">Создание подсети</span><span class="sxs-lookup"><span data-stu-id="75a0b-132">Create subnet</span></span>

<span data-ttu-id="75a0b-133">Новая подсеть добавляется toohello виртуальной сети с помощью hello [создать подсеть виртуальной сети сети az](/cli/azure/network/vnet/subnet#create) команды.</span><span class="sxs-lookup"><span data-stu-id="75a0b-133">A new subnet is added toohello virtual network using hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="75a0b-134">В этом примере hello подсеть с именем *mySubnetBackEnd* и задан префикс адреса *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="75a0b-134">In this example, hello subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="75a0b-135">Она используется со всеми внутренними службами.</span><span class="sxs-lookup"><span data-stu-id="75a0b-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="75a0b-136">На этом этапе мы создали сеть и разбили ее на две подсети — одна для интерфейсных служб, а вторая для внутренних служб.</span><span class="sxs-lookup"><span data-stu-id="75a0b-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="75a0b-137">В следующем разделе hello виртуальные машины создаются и подключенных toothese подсетей.</span><span class="sxs-lookup"><span data-stu-id="75a0b-137">In hello next section, virtual machines are created and connected toothese subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="75a0b-138">Общие сведения об общедоступном IP-адресе</span><span class="sxs-lookup"><span data-stu-id="75a0b-138">Understand public IP address</span></span>

<span data-ttu-id="75a0b-139">Общедоступный IP-адрес позволяет toobe ресурсы Azure доступны на hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="75a0b-139">A public IP address allows Azure resources toobe accessible on hello internet.</span></span> <span data-ttu-id="75a0b-140">В этом разделе учебника hello виртуальной Машины создается toodemonstrate как toowork с общедоступным IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="75a0b-140">In this section of hello tutorial, a VM is created toodemonstrate how toowork with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="75a0b-141">Способ выделения</span><span class="sxs-lookup"><span data-stu-id="75a0b-141">Allocation method</span></span>

<span data-ttu-id="75a0b-142">Общедоступный IP-адрес может быть динамическим или статическим.</span><span class="sxs-lookup"><span data-stu-id="75a0b-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="75a0b-143">По умолчанию выделяется динамический общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="75a0b-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="75a0b-144">После освобождения виртуальной машины освобождаются также и динамические IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="75a0b-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="75a0b-145">Это приводит к возникновению hello IP адрес toochange во время любой операции, которая включает в себя освобождения виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="75a0b-145">This behavior causes hello IP address toochange during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="75a0b-146">метод распределения Hello можно задать toostatic, гарантирует, что IP-адрес hello остаются назначенный tooa виртуальной Машины, даже во время освобождена состояния.</span><span class="sxs-lookup"><span data-stu-id="75a0b-146">hello allocation method can be set toostatic, which ensures that hello IP address remain assigned tooa VM, even during a deallocated state.</span></span> <span data-ttu-id="75a0b-147">При использовании статически выделенный IP-адрес, hello IP-адрес не указан.</span><span class="sxs-lookup"><span data-stu-id="75a0b-147">When using a statically allocated IP address, hello IP address itself cannot be specified.</span></span> <span data-ttu-id="75a0b-148">Он выделяется из пула доступных адресов.</span><span class="sxs-lookup"><span data-stu-id="75a0b-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="75a0b-149">Динамическое выделение</span><span class="sxs-lookup"><span data-stu-id="75a0b-149">Dynamic allocation</span></span>

<span data-ttu-id="75a0b-150">При создании виртуальной Машины с помощью hello [создания виртуальной машины az](/cli/azure/vm#create) команды выделения способ hello по умолчанию открытый IP-адреса является динамическим.</span><span class="sxs-lookup"><span data-stu-id="75a0b-150">When creating a VM with hello [az vm create](/cli/azure/vm#create) command, hello default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="75a0b-151">В следующем примере hello виртуальная машина создается с динамический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="75a0b-151">In hello following example, a VM is created with a dynamic IP address.</span></span> 

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

### <a name="static-allocation"></a><span data-ttu-id="75a0b-152">Статическое выделение</span><span class="sxs-lookup"><span data-stu-id="75a0b-152">Static allocation</span></span>

<span data-ttu-id="75a0b-153">При создании виртуальной машины, с помощью hello [создания виртуальной машины az](/cli/azure/vm#create) , укажите hello `--public-ip-address-allocation static` tooassign аргумент статический общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="75a0b-153">When creating a virtual machine using hello [az vm create](/cli/azure/vm#create) command, include hello `--public-ip-address-allocation static` argument tooassign a static public IP address.</span></span> <span data-ttu-id="75a0b-154">Эта операция не рассматривается в этом учебнике, однако в следующем разделе hello динамически выделенный IP-адрес измененные tooa статически выделяется адрес.</span><span class="sxs-lookup"><span data-stu-id="75a0b-154">This operation is not demonstrated in this tutorial, however in hello next section a dynamically allocated IP address is changed tooa statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="75a0b-155">Изменение метода выделения</span><span class="sxs-lookup"><span data-stu-id="75a0b-155">Change allocation method</span></span>

<span data-ttu-id="75a0b-156">можно изменить способ распределения Hello IP-адреса с помощью hello [обновления открытого ip-сети az](/cli/azure/network/public-ip#update) команды.</span><span class="sxs-lookup"><span data-stu-id="75a0b-156">hello IP address allocation method can be changed using hello [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="75a0b-157">В этом примере hello способ выделения IP-адреса из интерфейса ВМ изменяется hello toostatic.</span><span class="sxs-lookup"><span data-stu-id="75a0b-157">In this example, hello IP address allocation method of hello front-end VM is changed toostatic.</span></span>

<span data-ttu-id="75a0b-158">Во-первых освобождается hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="75a0b-158">First, deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="75a0b-159">Используйте hello [обновления открытого ip-сети az](/cli/azure/network/public-ip#update) команды tooupdate способ распределения hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-159">Use hello [az network public-ip update](/cli/azure/network/public-ip#update) command tooupdate hello allocation method.</span></span> <span data-ttu-id="75a0b-160">В этом случае hello `--allocation-method` задано слишком*статических*.</span><span class="sxs-lookup"><span data-stu-id="75a0b-160">In this case, hello `--allocation-method` is being set too*static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="75a0b-161">Запустите hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="75a0b-161">Start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="75a0b-162">Создание виртуальной машины без общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="75a0b-162">No public IP address</span></span>

<span data-ttu-id="75a0b-163">Часто, виртуальная машина не обязательно toobe доступно по Интернету hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-163">Often, a VM does not need toobe accessible over hello internet.</span></span> <span data-ttu-id="75a0b-164">toocreate виртуальной Машины без общедоступный IP-адрес, используйте hello `--public-ip-address ""` аргумент с пустой набор двойных кавычек.</span><span class="sxs-lookup"><span data-stu-id="75a0b-164">toocreate a VM without a public IP address, use hello `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="75a0b-165">Эта конфигурация рассматривается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="75a0b-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="75a0b-166">защищают сетевой трафик;</span><span class="sxs-lookup"><span data-stu-id="75a0b-166">Secure network traffic</span></span>

<span data-ttu-id="75a0b-167">Группа безопасности сети (NSG) содержит список правил безопасности, которые разрешают или запрещают tooresources сетевого трафика, подключенных tooAzure виртуальных сетей (VNet).</span><span class="sxs-lookup"><span data-stu-id="75a0b-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooAzure Virtual Networks (VNet).</span></span> <span data-ttu-id="75a0b-168">Nsg может быть связан toosubnets или отдельных сетевых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="75a0b-168">NSGs can be associated toosubnets or individual network interfaces.</span></span> <span data-ttu-id="75a0b-169">Когда NSG связана с сетевым интерфейсом, оно применяется только для hello связанных виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="75a0b-169">When an NSG is associated with a network interface, it applies only hello associated VM.</span></span> <span data-ttu-id="75a0b-170">Когда NSG связанные tooa подсети, hello правила применяются tooall ресурсы подключенных toohello подсети.</span><span class="sxs-lookup"><span data-stu-id="75a0b-170">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="75a0b-171">Правила группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="75a0b-171">Network security group rules</span></span>

<span data-ttu-id="75a0b-172">Правила группы безопасности сети определяют сетевые порты, через которые разрешен или запрещен трафик.</span><span class="sxs-lookup"><span data-stu-id="75a0b-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="75a0b-173">Hello правила могут включать исходный и конечный диапазоны IP-адресов, так что трафик контролируется между определенными системами или подсети.</span><span class="sxs-lookup"><span data-stu-id="75a0b-173">hello rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="75a0b-174">Правилам также присваивается приоритет (от 1 до 4096),</span><span class="sxs-lookup"><span data-stu-id="75a0b-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="75a0b-175">Правила, вычисляются в порядке приоритета hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-175">Rules are evaluated in hello order of priority.</span></span> <span data-ttu-id="75a0b-176">Правило с приоритетом 100 оценивается перед правилом с приоритетом 200.</span><span class="sxs-lookup"><span data-stu-id="75a0b-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="75a0b-177">Все группы NSG содержат набор правил по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="75a0b-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="75a0b-178">правила по умолчанию Hello не может быть удалена, но так как они будут назначены hello самый низкий приоритет, они могут быть переопределены созданных вами правил hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-178">hello default rules cannot be deleted, but because they are assigned hello lowest priority, they can be overridden by hello rules that you create.</span></span>

- <span data-ttu-id="75a0b-179">**Виртуальная сеть.** Входящий и исходящий трафик виртуальной сети разрешен в обоих направлениях.</span><span class="sxs-lookup"><span data-stu-id="75a0b-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="75a0b-180">**Интернет.** Исходящий трафик разрешен, но входящий трафик заблокирован.</span><span class="sxs-lookup"><span data-stu-id="75a0b-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="75a0b-181">**Подсистема балансировки нагрузки** -работоспособности hello tooprobe подсистемы балансировки нагрузки Azure разрешить виртуальных машин и экземпляров ролей.</span><span class="sxs-lookup"><span data-stu-id="75a0b-181">**Load balancer** - Allow Azure’s load balancer tooprobe hello health of your VMs and role instances.</span></span> <span data-ttu-id="75a0b-182">Если набор балансировки нагрузки не используется, это правило можно переопределить.</span><span class="sxs-lookup"><span data-stu-id="75a0b-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="75a0b-183">Создание групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="75a0b-183">Create network security groups</span></span>

<span data-ttu-id="75a0b-184">Группы безопасности могут быть созданы на hello же время, что и ВМ с помощью hello [создания виртуальной машины az](/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="75a0b-184">A network security group can be created at hello same time as a VM using hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="75a0b-185">При этом hello NSG связан с сетевым интерфейсом hello виртуальных машин и правило NSG является созданы автоматически tooallow трафик через порт *22* из любого источника.</span><span class="sxs-lookup"><span data-stu-id="75a0b-185">When doing so, hello NSG is associated with hello VMs network interface and an NSG rule is auto created tooallow traffic on port *22* from any source.</span></span> <span data-ttu-id="75a0b-186">Ранее в этом учебнике приветствия переднего плана NSG был автоматически создан с hello интерфейса виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="75a0b-186">Earlier in this tutorial, hello front-end NSG was auto-created with hello front-end VM.</span></span> <span data-ttu-id="75a0b-187">Кроме того, было также создано правило NSG для порта 22.</span><span class="sxs-lookup"><span data-stu-id="75a0b-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="75a0b-188">В некоторых случаях может быть полезным toopre-создать NSG, например, когда не следует создавать правила по умолчанию SSH или когда hello NSG должно быть вложенных tooa подсети.</span><span class="sxs-lookup"><span data-stu-id="75a0b-188">In some cases, it may be helpful toopre-create an NSG, such as when default SSH rules should not be created, or when hello NSG should be attached tooa subnet.</span></span> 

<span data-ttu-id="75a0b-189">Используйте hello [создать az сети nsg](/cli/azure/network/nsg#create) toocreate команда группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="75a0b-189">Use hello [az network nsg create](/cli/azure/network/nsg#create) command toocreate a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="75a0b-190">Вместо того чтобы сопоставлять hello NSG tooa сетевого интерфейса, связанного с подсетью.</span><span class="sxs-lookup"><span data-stu-id="75a0b-190">Instead of associating hello NSG tooa network interface, it is associated with a subnet.</span></span> <span data-ttu-id="75a0b-191">В этой конфигурации все виртуальные Машины, вложенные toohello подсети наследует правила NSG hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-191">In this configuration, any VM that is attached toohello subnet inherits hello NSG rules.</span></span>

<span data-ttu-id="75a0b-192">Обновление существующей подсети hello с именем *mySubnetBackEnd* с новой NSG hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-192">Update hello existing subnet named *mySubnetBackEnd* with hello new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="75a0b-193">Теперь создайте виртуальную машину, являющийся вложенного toohello *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="75a0b-193">Now create a virtual machine, which is attached toohello *mySubnetBackEnd*.</span></span> <span data-ttu-id="75a0b-194">Обратите внимание, что hello `--nsg` аргумент имеет значение пустой двойных кавычек.</span><span class="sxs-lookup"><span data-stu-id="75a0b-194">Notice that hello `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="75a0b-195">NSG не обязательно toobe, созданных с помощью hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="75a0b-195">An NSG does not need toobe created with hello VM.</span></span> <span data-ttu-id="75a0b-196">Hello виртуальной Машины — вложенное toohello конечной подсети защищены с помощью предварительно созданного внутреннего интерфейса NSG hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-196">hello VM is attached toohello back-end subnet, which is protected with hello pre-created back-end NSG.</span></span> <span data-ttu-id="75a0b-197">Этот NSG применяется toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="75a0b-197">This NSG applies toohello VM.</span></span> <span data-ttu-id="75a0b-198">Кроме того, обратите внимание, что hello `--public-ip-address` аргумент имеет значение пустой двойных кавычек.</span><span class="sxs-lookup"><span data-stu-id="75a0b-198">Also, notice here that hello `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="75a0b-199">Эта конфигурация создает виртуальную машину без общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="75a0b-199">This configuration creates a VM without a public IP address.</span></span> 

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

### <a name="secure-incoming-traffic"></a><span data-ttu-id="75a0b-200">Защита входящего трафика</span><span class="sxs-lookup"><span data-stu-id="75a0b-200">Secure incoming traffic</span></span>

<span data-ttu-id="75a0b-201">Когда hello интерфейса виртуальной Машины была создана, tooallow входящий трафик через порт 22 было создано правило NSG.</span><span class="sxs-lookup"><span data-stu-id="75a0b-201">When hello front-end VM was created, an NSG rule was created tooallow incoming traffic on port 22.</span></span> <span data-ttu-id="75a0b-202">Это правило позволяет toohello подключений SSH виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="75a0b-202">This rule allows SSH connections toohello VM.</span></span> <span data-ttu-id="75a0b-203">В этом примере трафик также необходимо разрешить через порт *80*.</span><span class="sxs-lookup"><span data-stu-id="75a0b-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="75a0b-204">Эта конфигурация обеспечивает toobe приложения web, доступе к hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="75a0b-204">This configuration allows a web application toobe accessed on hello VM.</span></span>

<span data-ttu-id="75a0b-205">Используйте hello [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) toocreate команда правило для порта *80*.</span><span class="sxs-lookup"><span data-stu-id="75a0b-205">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port *80*.</span></span>

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

<span data-ttu-id="75a0b-206">Hello интерфейса виртуальной Машины, теперь доступны только через порт *22* и порт *80*.</span><span class="sxs-lookup"><span data-stu-id="75a0b-206">hello front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="75a0b-207">Весь входящий трафик блокируется в группы безопасности сети hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-207">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="75a0b-208">Может оказаться полезным toovisualize hello NSG правила конфигурации.</span><span class="sxs-lookup"><span data-stu-id="75a0b-208">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="75a0b-209">Конфигурация правила NSG возвращаемого hello с hello [список правил сетевой az](/cli/azure/network/nsg/rule#list) команды.</span><span class="sxs-lookup"><span data-stu-id="75a0b-209">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="75a0b-210">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="75a0b-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a><span data-ttu-id="75a0b-211">Защита виртуальной Машины tooVM трафика</span><span class="sxs-lookup"><span data-stu-id="75a0b-211">Secure VM tooVM traffic</span></span>

<span data-ttu-id="75a0b-212">Правила группы безопасности сети также можно применить между виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="75a0b-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="75a0b-213">В этом примере hello интерфейса виртуальной Машины требуется toocommunicate с hello внутренней виртуальной Машины на порте *22* и *3306*.</span><span class="sxs-lookup"><span data-stu-id="75a0b-213">For this example, hello front-end VM needs toocommunicate with hello back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="75a0b-214">Эта конфигурация позволяет соединений по протоколу SSH с hello интерфейса виртуальной Машины, а также позволяют приложению на hello переднего плана toocommunicate ВМ с внутренней базой данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="75a0b-214">This configuration allows SSH connections from hello front-end VM, and also allow an application on hello front-end VM toocommunicate with a back-end MySQL database.</span></span> <span data-ttu-id="75a0b-215">Должно быть заблокировано весь трафик между виртуальными машинами hello внешнего и внутреннего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="75a0b-215">All other traffic should be blocked between hello front-end and back-end virtual machines.</span></span>

<span data-ttu-id="75a0b-216">Используйте hello [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) toocreate команда правило для порта 22.</span><span class="sxs-lookup"><span data-stu-id="75a0b-216">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port 22.</span></span> <span data-ttu-id="75a0b-217">Обратите внимание, что hello `--source-address-prefix` аргумент задает значение *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="75a0b-217">Notice that hello `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="75a0b-218">Эта конфигурация гарантирует, что только из интерфейса подсети hello-трафика через hello NSG.</span><span class="sxs-lookup"><span data-stu-id="75a0b-218">This configuration ensures that only traffic from hello front-end subnet is allowed through hello NSG.</span></span>

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

<span data-ttu-id="75a0b-219">Теперь добавьте правило, разрешающее трафик MySQL через порт 3306.</span><span class="sxs-lookup"><span data-stu-id="75a0b-219">Now add a rule for MySQL traffic on port 3306.</span></span>

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

<span data-ttu-id="75a0b-220">Наконец, если у Nsg правило по умолчанию, что позволяет весь трафик между виртуальными машинами в hello же виртуальной сети, правила могут быть созданы для hello серверной части Nsg tooblock весь трафик.</span><span class="sxs-lookup"><span data-stu-id="75a0b-220">Finally, because NSGs have a default rule allowing all traffic between VMs in hello same VNet, a rule can be created for hello back-end NSGs tooblock all traffic.</span></span> <span data-ttu-id="75a0b-221">Обратите внимание, что hello `--priority` присваивается значение *300*, который меньше, что оба hello правила NSG и MySQL.</span><span class="sxs-lookup"><span data-stu-id="75a0b-221">Notice here that hello `--priority` is given a value of *300*, which is lower that both hello NSG and MySQL rules.</span></span> <span data-ttu-id="75a0b-222">Эта конфигурация гарантирует, что SSH и MySQL по-прежнему трафик через hello NSG.</span><span class="sxs-lookup"><span data-stu-id="75a0b-222">This configuration ensures that SSH and MySQL traffic is still allowed through hello NSG.</span></span>

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

<span data-ttu-id="75a0b-223">Hello внутренней виртуальной Машины, теперь доступны только через порт *22* и порт *3306* из интерфейса подсети hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-223">hello back-end VM is now only accessible on port *22* and port *3306* from hello front-end subnet.</span></span> <span data-ttu-id="75a0b-224">Весь входящий трафик блокируется в группы безопасности сети hello.</span><span class="sxs-lookup"><span data-stu-id="75a0b-224">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="75a0b-225">Может оказаться полезным toovisualize hello NSG правила конфигурации.</span><span class="sxs-lookup"><span data-stu-id="75a0b-225">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="75a0b-226">Конфигурация правила NSG возвращаемого hello с hello [список правил сетевой az](/cli/azure/network/nsg/rule#list) команды.</span><span class="sxs-lookup"><span data-stu-id="75a0b-226">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="75a0b-227">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="75a0b-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="75a0b-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="75a0b-228">Next steps</span></span>

<span data-ttu-id="75a0b-229">В этом учебнике создается и защищенных сетей Azure как связанные toovirtual машины.</span><span class="sxs-lookup"><span data-stu-id="75a0b-229">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> <span data-ttu-id="75a0b-230">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="75a0b-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75a0b-231">развертывать виртуальную сеть;</span><span class="sxs-lookup"><span data-stu-id="75a0b-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="75a0b-232">создавать подсеть в виртуальной сети;</span><span class="sxs-lookup"><span data-stu-id="75a0b-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="75a0b-233">Подключите виртуальные машины tooa подсети</span><span class="sxs-lookup"><span data-stu-id="75a0b-233">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="75a0b-234">управлять общедоступными IP-адресами виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="75a0b-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="75a0b-235">защищать входящий интернет-трафик;</span><span class="sxs-lookup"><span data-stu-id="75a0b-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="75a0b-236">Защита виртуальной Машины tooVM трафика</span><span class="sxs-lookup"><span data-stu-id="75a0b-236">Secure VM tooVM traffic</span></span>

<span data-ttu-id="75a0b-237">Переместить следующий учебник toolearn toohello о защите данных на виртуальных машинах с помощью резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="75a0b-237">Advance toohello next tutorial toolearn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="75a0b-238">Архивация виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="75a0b-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
