---
title: "Создание копии виртуальной машины Linux с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Узнайте, как создать копию виртуальной машины Linux в Azure, развернутой посредством модели Resource Manager, с помощью Azure CLI 1.0."
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
ms.openlocfilehash: 62ae54f3596c9383cbf3b401fcfdb42ecfdee63c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-the-azure-cli-10"></a><span data-ttu-id="d6871-103">Создание копии виртуальной машины Linux, работающей в Azure, с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d6871-103">Create a copy of a Linux virtual machine running on Azure with the Azure CLI 1.0</span></span>
<span data-ttu-id="d6871-104">В этой статье показано, как создать копию виртуальной машины Azure под управлением Linux, используя модель развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d6871-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Resource Manager deployment model.</span></span> <span data-ttu-id="d6871-105">Сначала следует скопировать операционную систему и диски данных в новый контейнер, а затем настроить сетевые ресурсы и создать новую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d6871-105">First you copy over the operating system and data disks to a new container, then set up the network resources and create the new virtual machine.</span></span>

<span data-ttu-id="d6871-106">Кроме того, можно [передать пользовательский образ диска и создать виртуальную машину на его основе](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6871-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="d6871-107">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="d6871-107">CLI versions to complete the task</span></span>
<span data-ttu-id="d6871-108">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="d6871-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="d6871-109">Azure CLI 1.0 — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="d6871-109">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="d6871-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d6871-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d6871-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="d6871-111">Before you begin</span></span>
<span data-ttu-id="d6871-112">Перед началом описанной ниже процедуры необходимо выполнить следующие условия.</span><span class="sxs-lookup"><span data-stu-id="d6871-112">Ensure that you meet the following prerequisites before you start the steps:</span></span>

* <span data-ttu-id="d6871-113">Необходимо скачать [интерфейс командной строки Azure (Azure CLI)](../../cli-install-nodejs.md) и установить его на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d6871-113">You have the [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="d6871-114">Необходимы также некоторые сведения о существующей виртуальной машине Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="d6871-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="d6871-115">Сведения об исходной виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="d6871-115">Source VM information</span></span> | <span data-ttu-id="d6871-116">Как получить</span><span class="sxs-lookup"><span data-stu-id="d6871-116">Where to get it</span></span> |
| --- | --- |
| <span data-ttu-id="d6871-117">Имя виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d6871-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="d6871-118">Имя группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="d6871-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="d6871-119">Расположение</span><span class="sxs-lookup"><span data-stu-id="d6871-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="d6871-120">Имя учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="d6871-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="d6871-121">Имя контейнера</span><span class="sxs-lookup"><span data-stu-id="d6871-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="d6871-122">Имя исходного VHD-файла виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d6871-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="d6871-123">Необходимо будет выбрать параметры новой виртуальной машины:    </span><span class="sxs-lookup"><span data-stu-id="d6871-123">You will need to make some choices about your new VM:    </span></span><br> <span data-ttu-id="d6871-124">- имя контейнера;    </span><span class="sxs-lookup"><span data-stu-id="d6871-124">-Container name    </span></span><br> <span data-ttu-id="d6871-125">- имя виртуальной машины;    </span><span class="sxs-lookup"><span data-stu-id="d6871-125">-VM name    </span></span><br> <span data-ttu-id="d6871-126">- размер виртуальной машины;    </span><span class="sxs-lookup"><span data-stu-id="d6871-126">-VM size    </span></span><br> <span data-ttu-id="d6871-127">- имя виртуальной сети;    </span><span class="sxs-lookup"><span data-stu-id="d6871-127">-vNet name    </span></span><br> <span data-ttu-id="d6871-128">- имя подсети;    </span><span class="sxs-lookup"><span data-stu-id="d6871-128">-SubNet name    </span></span><br> <span data-ttu-id="d6871-129">- имя IP-адреса;    </span><span class="sxs-lookup"><span data-stu-id="d6871-129">-IP Name    </span></span><br> <span data-ttu-id="d6871-130">- имя сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="d6871-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="d6871-131">Вход и задание подписки</span><span class="sxs-lookup"><span data-stu-id="d6871-131">Login and set your subscription</span></span>
1. <span data-ttu-id="d6871-132">Войдите в интерфейс командной строки.</span><span class="sxs-lookup"><span data-stu-id="d6871-132">Login to the CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="d6871-133">Убедитесь, что режим Resource Manager включен.</span><span class="sxs-lookup"><span data-stu-id="d6871-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="d6871-134">Задайте соответствующую подписку.</span><span class="sxs-lookup"><span data-stu-id="d6871-134">Set the correct subscription.</span></span> <span data-ttu-id="d6871-135">Для просмотра всех подписок можно использовать команду azure account list.</span><span class="sxs-lookup"><span data-stu-id="d6871-135">You can use 'azure account list' to see all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-the-vm"></a><span data-ttu-id="d6871-136">Остановка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d6871-136">Stop the VM</span></span>
<span data-ttu-id="d6871-137">Остановите исходную виртуальную машину и отмените ее распределение.</span><span class="sxs-lookup"><span data-stu-id="d6871-137">Stop and deallocate the source VM.</span></span> <span data-ttu-id="d6871-138">Для получения списка всех виртуальных машин в подписке и имен их групп ресурсов можно использовать команду azure vm list.</span><span class="sxs-lookup"><span data-stu-id="d6871-138">You can use 'azure vm list' to get a list of all of the VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-the-vhd"></a><span data-ttu-id="d6871-139">Копирование виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="d6871-139">Copy the VHD</span></span>
<span data-ttu-id="d6871-140">Скопировать виртуальный жесткий диск из исходного хранилища в место назначения можно с помощью команды `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="d6871-140">You can copy the VHD from the source storage to the destination using the `azure storage blob copy start`.</span></span> <span data-ttu-id="d6871-141">В этом примере мы скопируем виртуальный жесткий диск в ту же учетную запись хранения, но в другой контейнер.</span><span class="sxs-lookup"><span data-stu-id="d6871-141">In this example, we are going to copy the VHD to the same storage account, but a different container.</span></span>

<span data-ttu-id="d6871-142">Чтобы скопировать виртуальный жесткий диск в другой контейнер в той же учетной записи хранения, введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d6871-142">To copy the VHD to another container in the same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-the-virtual-network-for-your-new-vm"></a><span data-ttu-id="d6871-143">Настройка виртуальной сети для новой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d6871-143">Set up the virtual network for your new VM</span></span>
<span data-ttu-id="d6871-144">Настройте виртуальную сеть и сетевую карту для новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d6871-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-the-new-vm"></a><span data-ttu-id="d6871-145">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d6871-145">Create the new VM</span></span>
<span data-ttu-id="d6871-146">Теперь можно создать виртуальную машину из переданного виртуального диска, [используя шаблон Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) или интерфейс командной строки, указав универсальный код ресурса (URI) скопированного диска. Для этого введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d6871-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through the CLI by specifying the URI to your copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="d6871-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6871-147">Next steps</span></span>
<span data-ttu-id="d6871-148">Чтобы узнать, как использовать интерфейс командной строки Azure для управления новой виртуальной машиной, ознакомьтесь со статьей [Команды Azure CLI в режиме Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="d6871-148">To learn how to use Azure CLI to manage your new virtual machine, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

