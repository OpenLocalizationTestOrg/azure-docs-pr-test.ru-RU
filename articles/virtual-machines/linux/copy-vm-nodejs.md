---
title: "копия виртуальной Машины Linux с hello Azure CLI 1.0 aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate копию виртуальной машины с Azure Linux hello Azure CLI 1.0 в модели развертывания диспетчера ресурсов hello"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a><span data-ttu-id="64737-103">Создать копию виртуальной машины Linux, работающих в Azure с hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="64737-103">Create a copy of a Linux virtual machine running on Azure with hello Azure CLI 1.0</span></span>
<span data-ttu-id="64737-104">В этой статье показано, как toocreate копию вашей виртуальной машины (VM) Azure запущенным Linux с помощью hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="64737-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Resource Manager deployment model.</span></span> <span data-ttu-id="64737-105">Сначала копирования hello операционной системы и дисков tooa новый контейнер данных, а затем настроить ресурсы сети hello и создание новой виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="64737-105">First you copy over hello operating system and data disks tooa new container, then set up hello network resources and create hello new virtual machine.</span></span>

<span data-ttu-id="64737-106">Кроме того, можно [передать пользовательский образ диска и создать виртуальную машину на его основе](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="64737-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="64737-107">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="64737-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="64737-108">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="64737-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="64737-109">Azure CLI 1.0 — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="64737-109">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="64737-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="64737-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="64737-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="64737-111">Before you begin</span></span>
<span data-ttu-id="64737-112">Убедитесь, что выполнены следующие предварительные требования перед выполнением действий hello hello:</span><span class="sxs-lookup"><span data-stu-id="64737-112">Ensure that you meet hello following prerequisites before you start hello steps:</span></span>

* <span data-ttu-id="64737-113">У вас есть hello [Azure CLI](../../cli-install-nodejs.md) загружается и устанавливается на компьютере.</span><span class="sxs-lookup"><span data-stu-id="64737-113">You have hello [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="64737-114">Необходимы также некоторые сведения о существующей виртуальной машине Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="64737-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="64737-115">Сведения об исходной виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="64737-115">Source VM information</span></span> | <span data-ttu-id="64737-116">Где tooget его</span><span class="sxs-lookup"><span data-stu-id="64737-116">Where tooget it</span></span> |
| --- | --- |
| <span data-ttu-id="64737-117">имя виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="64737-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="64737-118">Имя группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="64737-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="64737-119">Расположение</span><span class="sxs-lookup"><span data-stu-id="64737-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="64737-120">Имя учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="64737-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="64737-121">Имя контейнера</span><span class="sxs-lookup"><span data-stu-id="64737-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="64737-122">Имя исходного VHD-файла виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="64737-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="64737-123">О новой виртуальной Машины потребуется toomake некоторые варианты:   </span><span class="sxs-lookup"><span data-stu-id="64737-123">You will need toomake some choices about your new VM:    </span></span><br> <span data-ttu-id="64737-124">- имя контейнера;    </span><span class="sxs-lookup"><span data-stu-id="64737-124">-Container name    </span></span><br> <span data-ttu-id="64737-125">- имя виртуальной машины;    </span><span class="sxs-lookup"><span data-stu-id="64737-125">-VM name    </span></span><br> <span data-ttu-id="64737-126">- размер виртуальной машины;    </span><span class="sxs-lookup"><span data-stu-id="64737-126">-VM size    </span></span><br> <span data-ttu-id="64737-127">- имя виртуальной сети;    </span><span class="sxs-lookup"><span data-stu-id="64737-127">-vNet name    </span></span><br> <span data-ttu-id="64737-128">- имя подсети;    </span><span class="sxs-lookup"><span data-stu-id="64737-128">-SubNet name    </span></span><br> <span data-ttu-id="64737-129">- имя IP-адреса;    </span><span class="sxs-lookup"><span data-stu-id="64737-129">-IP Name    </span></span><br> <span data-ttu-id="64737-130">- имя сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="64737-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="64737-131">Вход и задание подписки</span><span class="sxs-lookup"><span data-stu-id="64737-131">Login and set your subscription</span></span>
1. <span data-ttu-id="64737-132">Toohello входа CLI.</span><span class="sxs-lookup"><span data-stu-id="64737-132">Login toohello CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="64737-133">Убедитесь, что режим Resource Manager включен.</span><span class="sxs-lookup"><span data-stu-id="64737-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="64737-134">Задать hello нужной подписки.</span><span class="sxs-lookup"><span data-stu-id="64737-134">Set hello correct subscription.</span></span> <span data-ttu-id="64737-135">Можно использовать «учетная запись azure список» toosee всех подписок.</span><span class="sxs-lookup"><span data-stu-id="64737-135">You can use 'azure account list' toosee all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a><span data-ttu-id="64737-136">Остановить hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="64737-136">Stop hello VM</span></span>
<span data-ttu-id="64737-137">Остановка и освобождать hello исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="64737-137">Stop and deallocate hello source VM.</span></span> <span data-ttu-id="64737-138">«Список виртуальных машин azure» tooget список всех hello виртуальных машин можно использовать в вашей подписке и их имена групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="64737-138">You can use 'azure vm list' tooget a list of all of hello VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a><span data-ttu-id="64737-139">Скопируйте hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="64737-139">Copy hello VHD</span></span>
<span data-ttu-id="64737-140">Hello виртуального жесткого диска можно скопировать из хранилища toohello hello источник назначения с помощью hello `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="64737-140">You can copy hello VHD from hello source storage toohello destination using hello `azure storage blob copy start`.</span></span> <span data-ttu-id="64737-141">В этом примере мы будем toocopy hello VHD toohello учетную запись хранения, но другой контейнер.</span><span class="sxs-lookup"><span data-stu-id="64737-141">In this example, we are going toocopy hello VHD toohello same storage account, but a different container.</span></span>

<span data-ttu-id="64737-142">контейнер tooanother toocopy hello VHD в hello учетную запись хранения, введите:</span><span class="sxs-lookup"><span data-stu-id="64737-142">toocopy hello VHD tooanother container in hello same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a><span data-ttu-id="64737-143">Настроить виртуальную сеть hello для новой виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="64737-143">Set up hello virtual network for your new VM</span></span>
<span data-ttu-id="64737-144">Настройте виртуальную сеть и сетевую карту для новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="64737-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="64737-145">Создание новой виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="64737-145">Create hello new VM</span></span>
<span data-ttu-id="64737-146">Теперь можно создать виртуальную Машину из виртуального диска [с помощью шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) или через hello CLI, указав hello URI tooyour копирования дисков, введя:</span><span class="sxs-lookup"><span data-stu-id="64737-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through hello CLI by specifying hello URI tooyour copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="64737-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64737-147">Next steps</span></span>
<span data-ttu-id="64737-148">toolearn как toomanage Azure CLI toouse новой виртуальной машины в разделе [команды Azure CLI для диспетчера ресурсов Azure hello](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="64737-148">toolearn how toouse Azure CLI toomanage your new virtual machine, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

