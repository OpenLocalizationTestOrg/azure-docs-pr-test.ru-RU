---
title: "Виртуальная машина Linux с помощью Azure CLI 2.0 aaaCopy | Документы Microsoft"
description: "Узнайте, как toocreate копию ВМ Linux Azure с помощью Azure CLI 2.0 и управляемых дисков."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="891d0-103">Создание копии виртуальной машины Linux с помощью Azure CLI 2.0 и Управляемых дисков</span><span class="sxs-lookup"><span data-stu-id="891d0-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="891d0-104">В этой статье показано, как hello toocreate копии Azure виртуальной машины (VM) под управлением Linux с помощью Azure CLI 2.0 и модель развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="891d0-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Azure CLI 2.0 and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="891d0-105">Можно также выполнить следующие действия с hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="891d0-105">You can also perform these steps with hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="891d0-106">Кроме того, можно [передать VHD и создать виртуальную машину на его основе](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="891d0-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="891d0-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="891d0-107">Prerequisites</span></span>


-   <span data-ttu-id="891d0-108">Установка [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="891d0-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="891d0-109">Войдите в tooan учетная запись Azure с [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="891d0-109">Sign in tooan Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="891d0-110">Иметь toouse виртуальной Машины Azure в качестве hello источником для копии.</span><span class="sxs-lookup"><span data-stu-id="891d0-110">Have an Azure VM toouse as hello source for your copy.</span></span>

## <a name="step-1-stop-hello-source-vm"></a><span data-ttu-id="891d0-111">Шаг 1: Остановите hello исходной виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="891d0-111">Step 1: Stop hello source VM</span></span>


<span data-ttu-id="891d0-112">Освободить hello исходной виртуальной Машины с помощью [ВМ az deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="891d0-112">Deallocate hello source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="891d0-113">Hello следующий пример отменяет выделение hello виртуальной Машины с именем **myVM** в группе ресурсов hello **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="891d0-113">hello following example deallocates hello VM named **myVM** in hello resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a><span data-ttu-id="891d0-114">Шаг 2: Скопируйте hello исходной виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="891d0-114">Step 2: Copy hello source VM</span></span>


<span data-ttu-id="891d0-115">toocopy виртуальной Машины, можно создать копию hello базового виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="891d0-115">toocopy a VM, you create a copy of hello underlying virtual hard disk.</span></span> <span data-ttu-id="891d0-116">Этот процесс создает специализированные виртуального жесткого диска в качестве управляемого диска, содержащего hello одинаковые конфигурации и параметры, как hello исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="891d0-116">This process creates a specialized VHD as a Managed Disk that contains hello same configuration and settings as hello source VM.</span></span>

<span data-ttu-id="891d0-117">Дополнительные сведения об Управляемых дисках Azure см. в [обзоре Управляемых дисков Azure](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="891d0-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="891d0-118">Все имена виртуальных Машин и hello его диска операционной системы с [список виртуальных машин az](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="891d0-118">List each VM and hello name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="891d0-119">Hello следующий пример отображает список всех виртуальных машин в группе ресурсов с именем **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="891d0-119">hello following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="891d0-120">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="891d0-120">hello output is similar toohello following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="891d0-121">Копировать диск hello путем создания нового управляемого диска с помощью [создать диск az](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="891d0-121">Copy hello disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="891d0-122">Hello следующий пример создает диск с именем **myCopiedDisk** из hello управляемым диск с именем **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="891d0-122">hello following example creates a disk named **myCopiedDisk** from hello managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="891d0-123">Проверьте диски hello управляемых теперь в группе ресурсов с помощью [список дисков az](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="891d0-123">Verify hello managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="891d0-124">Hello в примере список управляемых hello дисков в группе ресурсов hello с именем **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="891d0-124">hello following example lists hello managed disks in hello resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="891d0-125">Пропустить слишком[«шаг 3: Настройка виртуальной сети»](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="891d0-125">Skip too["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="891d0-126">Шаг 3. Настройка виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="891d0-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="891d0-127">Hello следующих дополнительных шагов создания новой виртуальной сети, подсети, общедоступный IP-адрес и виртуальный сетевой адаптер (NIC).</span><span class="sxs-lookup"><span data-stu-id="891d0-127">hello following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="891d0-128">При копировании виртуальной Машины для устранения неполадок или дополнительные развертывания, вы можете не toouse виртуальной Машины в существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="891d0-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want toouse a VM in an existing virtual network.</span></span>

<span data-ttu-id="891d0-129">Если требуется toocreate инфраструктуре виртуальной сети для виртуальных машин скопированный выполните рядом hello несколько действий.</span><span class="sxs-lookup"><span data-stu-id="891d0-129">If you want toocreate a virtual network infrastructure for your copied VMs, follow hello next few steps.</span></span> <span data-ttu-id="891d0-130">Если вы не хотите toocreate виртуальную сеть, пропустите слишком[шаг 4: создайте виртуальную Машину](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="891d0-130">If you don't want toocreate a virtual network, skip too[Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="891d0-131">Создайте виртуальную сеть hello с помощью [создания az сети vnet](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="891d0-131">Create hello virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="891d0-132">Hello следующий пример создает виртуальную сеть с именем **myVnet** и подсеть с именем **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="891d0-132">hello following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="891d0-133">Создайте общедоступный IP-адрес, выполнив команду [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="891d0-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="891d0-134">Hello следующий пример создает общедоступный IP-адрес с именем **myPublicIP** с именем DNS hello **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="891d0-134">hello following example creates a public IP named **myPublicIP** with hello DNS name of **mypublicdns**.</span></span> <span data-ttu-id="891d0-135">(hello DNS-имя должно быть уникальным, поэтому введите уникальное имя).</span><span class="sxs-lookup"><span data-stu-id="891d0-135">(hello DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="891d0-136">Создание с помощью Сетевых hello [Создание сетевого адаптера сети az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="891d0-136">Create hello NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="891d0-137">Hello следующий пример создает сетевой Адаптер с именем **myNic** с присоединенного toothe **mySubnet** подсети:</span><span class="sxs-lookup"><span data-stu-id="891d0-137">hello following example creates a NIC named **myNic** that's attached toothe **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="891d0-138">Шаг 4. Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="891d0-138">Step 4: Create a VM</span></span>

<span data-ttu-id="891d0-139">Теперь можно создать виртуальную машину, выполнив команду [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="891d0-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="891d0-140">Указать hello Копировать toouse управляемого диск как диск ОС hello (--присоединить os диск), как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="891d0-140">Specify hello copied managed disk toouse as hello OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="891d0-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="891d0-141">Next steps</span></span>

<span data-ttu-id="891d0-142">toolearn как toomanage Azure CLI toouse новых виртуальных Машин, в разделе [команды Azure CLI для диспетчера ресурсов Azure hello](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="891d0-142">toolearn how toouse Azure CLI toomanage your new VM, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
