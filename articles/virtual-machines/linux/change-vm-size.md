---
title: "Как изменить размер виртуальной машины Linux с помощью Azure CLI 2.0 | Документация Майкрософт"
description: "В статье рассматривается, как увеличить и уменьшить масштаб виртуальной машины Linux, изменяя ее размер."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23fc9f7f34732079682857d4ee685fe811751698
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="a567b-103">Изменение размера виртуальной машины Linux с помощью CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a567b-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="a567b-104">После того как вы подготовили виртуальную машину, ее можно увеличить или уменьшить, изменив [размер][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="a567b-104">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="a567b-105">В некоторых случаях сначала необходимо освободить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="a567b-105">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="a567b-106">Необходимо завершить общение с виртуальной машиной, если требуемый размер недоступен в кластере оборудования, в котором она размещена.</span><span class="sxs-lookup"><span data-stu-id="a567b-106">You need to deallocate the VM if the desired size is not available on the hardware cluster that is hosting the VM.</span></span> <span data-ttu-id="a567b-107">В этой статье описано, как изменить размер виртуальной машины Linux с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a567b-107">This article details how to resize a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="a567b-108">Эти действия можно также выполнить с помощью [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a567b-108">You can also perform these steps with the [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="a567b-109">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="a567b-109">Resize a VM</span></span>
<span data-ttu-id="a567b-110">Чтобы изменить размер виртуальной машины, нужно установить последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="a567b-110">To resize a VM, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="a567b-111">Выведите список размеров виртуальной машины, доступных в кластере оборудования, в котором она размещена, с помощью команды [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="a567b-111">View the list of available VM sizes on the hardware cluster where the VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="a567b-112">В следующем примере содержится список размеров виртуальных машин с именем `myVM` в группе ресурсов `myResourceGroup` региона:</span><span class="sxs-lookup"><span data-stu-id="a567b-112">The following example lists VM sizes for the VM named `myVM` in the resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="a567b-113">Если в списке есть нужный размер, выполните команду [az vm resize](/cli/azure/vm#resize), чтобы изменить размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a567b-113">If the desired VM size is listed, resize the VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="a567b-114">В следующем примере размер виртуальной машины с именем `myVM` изменяется до размера `Standard_DS3_v2`:</span><span class="sxs-lookup"><span data-stu-id="a567b-114">The following example resizes the VM named `myVM` to the `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="a567b-115">Во время этого процесса виртуальная машина перезагружается.</span><span class="sxs-lookup"><span data-stu-id="a567b-115">The VM restarts during this process.</span></span> <span data-ttu-id="a567b-116">После перезагрузки существующие диски ОС и данных переназначаются.</span><span class="sxs-lookup"><span data-stu-id="a567b-116">After the restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="a567b-117">Данные на временном диске будут утеряны.</span><span class="sxs-lookup"><span data-stu-id="a567b-117">Anything on the temporary disk is lost.</span></span>

3. <span data-ttu-id="a567b-118">Если требуемый размер виртуальной машины отсутствует в списке, сначала необходимо завершить общение с виртуальной машиной, используя команду [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="a567b-118">If the desired VM size is not listed, you need to first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="a567b-119">Этот процесс позволяет изменить размер виртуальной машины до любого значения, которое поддерживает регион, а затем перезапустить ее.</span><span class="sxs-lookup"><span data-stu-id="a567b-119">This process allows the VM to then be resized to any size available that the region supports and then started.</span></span> <span data-ttu-id="a567b-120">В следующих шагах завершается общение с виртуальной машиной `myVM` в группе ресурсов `myResourceGroup`, она масштабируется, а затем запускается.</span><span class="sxs-lookup"><span data-stu-id="a567b-120">The following steps deallocate, resize, and then start the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="a567b-121">Освобождение виртуальной машины также освобождает все назначенные ей динамические IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="a567b-121">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="a567b-122">Это не влияет на диски ОС и данных.</span><span class="sxs-lookup"><span data-stu-id="a567b-122">The OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a567b-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a567b-123">Next steps</span></span>
<span data-ttu-id="a567b-124">Для дополнительной масштабируемости запустите несколько экземпляров виртуальных машин и разверните их.</span><span class="sxs-lookup"><span data-stu-id="a567b-124">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="a567b-125">Дополнительные сведения см. в статье [Автоматическое масштабирование машин Linux в наборе масштабирования виртуальных машин][scale-set].</span><span class="sxs-lookup"><span data-stu-id="a567b-125">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
