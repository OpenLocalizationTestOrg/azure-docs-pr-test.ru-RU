---
title: "tooresize PowerShell aaaUse виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Измените размер виртуальной машины Windows, созданных в модели развертывания диспетчера ресурсов hello, с помощью Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: a4a80f3bc99911e4f1a095f0ce63aca00fa50694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="533c4-103">Изменение размера виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="533c4-103">Resize a Windows VM</span></span>
<span data-ttu-id="533c4-104">В этой статье показано, как tooresize ВМ Windows, созданные в hello диспетчера ресурсов развертывания модели с помощью Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="533c4-104">This article shows you how tooresize a Windows VM, created in hello Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="533c4-105">После создания виртуальной машины (VM), можно масштабировать hello ВМ вверх или вниз, изменив размер виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="533c4-105">After you create a virtual machine (VM), you can scale hello VM up or down by changing hello VM size.</span></span> <span data-ttu-id="533c4-106">В некоторых случаях необходимо сначала отменить hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="533c4-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="533c4-107">Это может произойти, если новый размер hello недоступен в кластере hello оборудования, который в настоящий момент размещена hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="533c4-107">This can happen if hello new size is not available on hello hardware cluster that is currently hosting hello VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="533c4-108">Изменение размера виртуальной машины Windows, не входящей в группу доступности</span><span class="sxs-lookup"><span data-stu-id="533c4-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="533c4-109">Список размеров hello виртуальных Машин, доступных на hello оборудования кластера, где размещается hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="533c4-109">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="533c4-110">При желании hello, указан размер выполните следующие команды tooresize hello ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="533c4-110">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="533c4-111">Если hello требуемого размера не указан, перейдите на toostep 3.</span><span class="sxs-lookup"><span data-stu-id="533c4-111">If hello desired size is not listed, go on toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="533c4-112">Если hello требуемого размера не указан, выполните следующие команды toodeallocate hello виртуальной Машины, ее размер и перезапуска ВМ hello hello.</span><span class="sxs-lookup"><span data-stu-id="533c4-112">If hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and restart hello VM.</span></span>
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> <span data-ttu-id="533c4-113">Освобождение hello ВМ освобождает любой динамических IP-адресов, назначенных toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="533c4-113">Deallocating hello VM releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="533c4-114">Hello ОС и диски с данными не затрагиваются.</span><span class="sxs-lookup"><span data-stu-id="533c4-114">hello OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="533c4-115">Изменение размера виртуальной машины Windows в группе доступности</span><span class="sxs-lookup"><span data-stu-id="533c4-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="533c4-116">Если hello новый размер для виртуальной Машины в наборе доступности не доступен на hello оборудования кластера в настоящее время размещается hello виртуальной Машины, а затем все виртуальные машины в наборе доступности hello потребуется toobe освобождена tooresize hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="533c4-116">If hello new size for a VM in an availability set is not available on hello hardware cluster currently hosting hello VM, then all VMs in hello availability set will need toobe deallocated tooresize hello VM.</span></span> <span data-ttu-id="533c4-117">Также может потребоваться размер hello tooupdate других виртуальных машин в доступности hello после одна виртуальная машина был изменен.</span><span class="sxs-lookup"><span data-stu-id="533c4-117">You also might need tooupdate hello size of other VMs in hello availability set after one VM has been resized.</span></span> <span data-ttu-id="533c4-118">tooresize виртуальной Машины в группу доступности выполнить следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="533c4-118">tooresize a VM in an availability set, perform hello following steps.</span></span>

1. <span data-ttu-id="533c4-119">Список размеров hello виртуальных Машин, доступных на hello оборудования кластера, где размещается hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="533c4-119">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="533c4-120">При желании hello, указан размер выполните следующие команды tooresize hello ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="533c4-120">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="533c4-121">Если нет, перейдите toostep 3.</span><span class="sxs-lookup"><span data-stu-id="533c4-121">If it is not listed, go toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="533c4-122">Если hello требуемого размера не указан, продолжите следующие шаги toodeallocate hello всех виртуальных машин в группе доступности hello, изменении размера виртуальной машины и перезапустить их.</span><span class="sxs-lookup"><span data-stu-id="533c4-122">If hello desired size is not listed, continue with hello following steps toodeallocate all VMs in hello availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="533c4-123">Остановите все виртуальные машины в наборе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="533c4-123">Stop all VMs in hello availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. <span data-ttu-id="533c4-124">Изменение размера и перезапустите hello виртуальных машин в группе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="533c4-124">Resize and restart hello VMs in hello availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a><span data-ttu-id="533c4-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="533c4-125">Next steps</span></span>
* <span data-ttu-id="533c4-126">Для дополнительной масштабируемости запустите несколько экземпляров виртуальных машин и разверните их. Дополнительные сведения см. в разделе [Автоматическое масштабирование ВМ в наборе масштабирования ВМ](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="533c4-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

