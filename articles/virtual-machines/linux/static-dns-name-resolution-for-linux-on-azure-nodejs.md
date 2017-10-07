---
title: "aaaUsing внутренние DNS для виртуальной Машины имен в Azure | Документы Microsoft"
description: "Использование внутренней службы DNS для разрешения имен виртуальных машин в Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="79044-103">Использование внутренней службы DNS для разрешения имен виртуальных машин в Azure</span><span class="sxs-lookup"><span data-stu-id="79044-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="79044-104">В этой статье показано, как tooset статические внутренние DNS имена виртуальных машин Linux с использованием карт виртуального сетевого Адаптера (VNic) и метка DNS-имена.</span><span class="sxs-lookup"><span data-stu-id="79044-104">This article shows how tooset static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="79044-105">Статические имена DNS используются для постоянных инфраструктурных служб, таких как сервер сборки Jenkins, который используется для этого поддержания документа, или сервер Git.</span><span class="sxs-lookup"><span data-stu-id="79044-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="79044-106">Существуют следующие требования Hello.</span><span class="sxs-lookup"><span data-stu-id="79044-106">hello requirements are:</span></span>

* <span data-ttu-id="79044-107">[учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="79044-107">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* <span data-ttu-id="79044-108">[файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="79044-108">[SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="79044-109">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="79044-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="79044-110">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="79044-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="79044-111">[Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="79044-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="79044-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="79044-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="79044-113">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="79044-113">Quick commands</span></span>

<span data-ttu-id="79044-114">Если вам требуется tooquickly выполнения задачи hello, hello в следующем разделе подробно описываются hello команд, которые необходимы.</span><span class="sxs-lookup"><span data-stu-id="79044-114">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="79044-115">Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="79044-115">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="79044-116">Предварительные требования: группа ресурсов, виртуальная сеть, группа безопасности сети с входящим трафиком SSH, подсеть.</span><span class="sxs-lookup"><span data-stu-id="79044-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="79044-117">Создание виртуального сетевого адаптера со статическим внутренним именем DNS</span><span class="sxs-lookup"><span data-stu-id="79044-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="79044-118">Hello `-r` cli флаг предназначен для параметра hello DNS метку, которую предоставляет hello статических DNS-имя для hello виртуального сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="79044-118">hello `-r` cli flag is for setting hello DNS label, which provides hello static DNS name for hello VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a><span data-ttu-id="79044-119">Развертывание hello виртуальной Машины в hello виртуальной сети, NSG и подключения hello виртуального сетевого адаптера</span><span class="sxs-lookup"><span data-stu-id="79044-119">Deploy hello VM into hello VNet, NSG and, connect hello VNic</span></span>

<span data-ttu-id="79044-120">Hello `-N` подключается hello виртуального сетевого адаптера toohello новой виртуальной Машины во время развертывания tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="79044-120">hello `-N` connects hello VNic toohello new VM during hello deployment tooAzure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="79044-121">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="79044-121">Detailed walkthrough</span></span>

<span data-ttu-id="79044-122">Полная непрерывной интеграции и непрерывного развертывания (CiCd) инфраструктуру в Azure требует определенных серверов toobe статической или долгоживущие серверов.</span><span class="sxs-lookup"><span data-stu-id="79044-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span>  <span data-ttu-id="79044-123">Рекомендуется, активов Azure как hello виртуальных сетей (Vnet) и группы безопасности сети (Nsg), должен быть статическим и долго ресурсы, которые развертываются редко.</span><span class="sxs-lookup"><span data-stu-id="79044-123">It is recommended that Azure assets like hello Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="79044-124">После развертывания виртуальной сети, он может быть использован в новые развертывания без инфраструктуры toohello любой негативно влияет на.</span><span class="sxs-lookup"><span data-stu-id="79044-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span>  <span data-ttu-id="79044-125">Добавление статического сети toothis Git репозитория сервер и сервер автоматизации Jenkins доставляет CiCd tooyour средах разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="79044-125">Adding toothis static network a Git repository server and a Jenkins automation server delivers CiCd tooyour development or test environments.</span></span>  

<span data-ttu-id="79044-126">Внутренние имена DNS можно сопоставлять только внутри виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="79044-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="79044-127">Так как hello DNS-имена являются внутренними, они не удается разрешить toohello за пределами Интернет, обеспечивая дополнительную безопасность инфраструктуры toohello.</span><span class="sxs-lookup"><span data-stu-id="79044-127">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="79044-128">_Замените все примеры своими именами._</span><span class="sxs-lookup"><span data-stu-id="79044-128">_Replace any examples with your own naming._</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="79044-129">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="79044-129">Create hello Resource group</span></span>

<span data-ttu-id="79044-130">Группа ресурсов находится необходимые tooorganize все, что мы создадим в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="79044-130">A Resource Group is needed tooorganize everything we create in this walkthrough.</span></span>  <span data-ttu-id="79044-131">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="79044-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="79044-132">Создать hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="79044-132">Create hello VNet</span></span>

<span data-ttu-id="79044-133">Hello первым шагом является toobuild виртуальных машин в hello toolaunch виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="79044-133">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span>  <span data-ttu-id="79044-134">Hello виртуальная сеть содержит одну подсеть для этого пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="79044-134">hello VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="79044-135">Дополнительные сведения о виртуальных сетях Azure см. в разделе [Создание виртуальной сети с помощью hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="79044-135">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a><span data-ttu-id="79044-136">Создать hello NSG</span><span class="sxs-lookup"><span data-stu-id="79044-136">Create hello NSG</span></span>

<span data-ttu-id="79044-137">Hello подсети создана за существующей сетевой группы безопасности, поэтому мы создаем hello NSG перед hello подсети.</span><span class="sxs-lookup"><span data-stu-id="79044-137">hello Subnet is built behind an existing Network Security Group so we build hello NSG before hello Subnet.</span></span>  <span data-ttu-id="79044-138">Nsg Azure — это эквивалент tooa брандмауэра на уровне сети hello.</span><span class="sxs-lookup"><span data-stu-id="79044-138">Azure NSGs are equivalent tooa firewall at hello network layer.</span></span>  <span data-ttu-id="79044-139">Дополнительные сведения о Nsg Azure см. в разделе [как Nsg toocreate в hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="79044-139">For more information on Azure NSGs, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="79044-140">Добавление правила, разрешающего входящий трафик по протоколу SSH</span><span class="sxs-lookup"><span data-stu-id="79044-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="79044-141">Hello ВМ Linux требуется доступ из hello необходима Интернета, переданной правило, разрешающее трафик 22 toobe входящий порт на виртуальной Машине Linux hello tooport сети hello 22.</span><span class="sxs-lookup"><span data-stu-id="79044-141">hello Linux VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="79044-142">Добавить toohello подсети виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="79044-142">Add a subnet toohello VNet</span></span>

<span data-ttu-id="79044-143">Виртуальные машины в виртуальной сети hello должна находиться в подсети.</span><span class="sxs-lookup"><span data-stu-id="79044-143">VMs within hello VNet must be located in a subnet.</span></span>  <span data-ttu-id="79044-144">Каждая виртуальная сеть может содержать несколько подсетей.</span><span class="sxs-lookup"><span data-stu-id="79044-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="79044-145">Создать подсеть hello и свяжите с tooadd NSG hello подсети toohello брандмауэра hello подсеть.</span><span class="sxs-lookup"><span data-stu-id="79044-145">Create hello subnet and associate hello subnet with hello NSG tooadd a firewall toohello subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="79044-146">Теперь Hello подсети добавляется внутри hello виртуальной сети и связанные с hello NSG и правила NSG hello.</span><span class="sxs-lookup"><span data-stu-id="79044-146">hello Subnet is now added inside hello VNet and associated with hello NSG and hello NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="79044-147">Создание статических DNS-имен</span><span class="sxs-lookup"><span data-stu-id="79044-147">Creating static DNS names</span></span>

<span data-ttu-id="79044-148">Azure является более гибким, но toouse DNS-имен для разрешения имен виртуальных машин, необходимо их как виртуальные сетевые карты (VNics) с помощью DNS пометки toocreate.</span><span class="sxs-lookup"><span data-stu-id="79044-148">Azure is very flexible, but toouse DNS names for VMs name resolution, you need toocreate them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="79044-149">VNics являются важными, как можно повторно использовать их, подключив их toodifferent ВМ, поддерживающий hello виртуального сетевого адаптера как статический ресурс hello виртуальных машин может быть временной.</span><span class="sxs-lookup"><span data-stu-id="79044-149">VNics are important as you can reuse them by connecting them toodifferent VMs, which keeps hello VNic as a static resource while hello VMs can be temporary.</span></span>  <span data-ttu-id="79044-150">С помощью DNS, метки на hello виртуального сетевого адаптера, не может tooenable простое имя разрешения из других виртуальных машин в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="79044-150">By using DNS labeling on hello VNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span>  <span data-ttu-id="79044-151">С помощью разрешения имен включает другие виртуальные машины сервера автоматизации hello tooaccess hello DNS-именем `Jenkins` или сервера hello Git в качестве `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="79044-151">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  <span data-ttu-id="79044-152">Создание виртуального сетевого адаптера и связать его с hello подсети, созданного в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="79044-152">Create a VNic and associate it with hello Subnet created in hello previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="79044-153">Развертывание hello виртуальной Машины в виртуальной сети hello и NSG</span><span class="sxs-lookup"><span data-stu-id="79044-153">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="79044-154">Теперь у нас есть виртуальной сети, подсети в этой виртуальной сети и NSG выступает в роли tooprotect брандмауэра нашей подсети, блокируя весь входящий трафик, за исключением порт 22 для SSH.</span><span class="sxs-lookup"><span data-stu-id="79044-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="79044-155">Теперь может быть развернут Hello виртуальной Машины внутри этой существующей сетевой инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="79044-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="79044-156">С помощью Azure CLI hello и hello `azure vm create` команды hello виртуальных Машин Linux — развернутой toohello существующие группы ресурсов Azure, виртуальной сети, подсети и виртуального сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="79044-156">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="79044-157">Дополнительные сведения об использовании toodeploy CLI hello завершения виртуальной Машины в разделе [создать полную среду Linux с помощью hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="79044-157">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="79044-158">С помощью hello CLI флаги toocall существующие ресурсы мы поручить Azure toodeploy hello виртуальных Машин в существующей сети hello.</span><span class="sxs-lookup"><span data-stu-id="79044-158">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span>  <span data-ttu-id="79044-159">tooreiterate, после развертывания виртуальной сети и подсети они могут остаться статические или постоянным ресурсов в ваш регион Azure.</span><span class="sxs-lookup"><span data-stu-id="79044-159">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="79044-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79044-160">Next steps</span></span>
* [<span data-ttu-id="79044-161">Создание полной среды Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="79044-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="79044-162">Создание виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="79044-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
