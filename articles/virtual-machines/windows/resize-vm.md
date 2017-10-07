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
# <a name="resize-a-windows-vm"></a>Изменение размера виртуальной машины Windows
В этой статье показано, как tooresize ВМ Windows, созданные в hello диспетчера ресурсов развертывания модели с помощью Azure Powershell.

После создания виртуальной машины (VM), можно масштабировать hello ВМ вверх или вниз, изменив размер виртуальной Машины hello. В некоторых случаях необходимо сначала отменить hello виртуальной Машины. Это может произойти, если новый размер hello недоступен в кластере hello оборудования, который в настоящий момент размещена hello виртуальной Машины.

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>Изменение размера виртуальной машины Windows, не входящей в группу доступности
1. Список размеров hello виртуальных Машин, доступных на hello оборудования кластера, где размещается hello виртуальной Машины. 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. При желании hello, указан размер выполните следующие команды tooresize hello ВМ hello. Если hello требуемого размера не указан, перейдите на toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Если hello требуемого размера не указан, выполните следующие команды toodeallocate hello виртуальной Машины, ее размер и перезапуска ВМ hello hello.
   
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
> Освобождение hello ВМ освобождает любой динамических IP-адресов, назначенных toohello виртуальной Машины. Hello ОС и диски с данными не затрагиваются. 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>Изменение размера виртуальной машины Windows в группе доступности
Если hello новый размер для виртуальной Машины в наборе доступности не доступен на hello оборудования кластера в настоящее время размещается hello виртуальной Машины, а затем все виртуальные машины в наборе доступности hello потребуется toobe освобождена tooresize hello виртуальной Машины. Также может потребоваться размер hello tooupdate других виртуальных машин в доступности hello после одна виртуальная машина был изменен. tooresize виртуальной Машины в группу доступности выполнить следующие шаги hello.

1. Список размеров hello виртуальных Машин, доступных на hello оборудования кластера, где размещается hello виртуальной Машины.
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. При желании hello, указан размер выполните следующие команды tooresize hello ВМ hello. Если нет, перейдите toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Если hello требуемого размера не указан, продолжите следующие шаги toodeallocate hello всех виртуальных машин в группе доступности hello, изменении размера виртуальной машины и перезапустить их.
4. Остановите все виртуальные машины в наборе доступности hello.
   
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
5. Изменение размера и перезапустите hello виртуальных машин в группе доступности hello.
   
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

## <a name="next-steps"></a>Дальнейшие действия
* Для дополнительной масштабируемости запустите несколько экземпляров виртуальных машин и разверните их. Дополнительные сведения см. в разделе [Автоматическое масштабирование ВМ в наборе масштабирования ВМ](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).

