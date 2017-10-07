---
title: "виртуальной машине из неуправляемого aaaConvert диски toomanaged - управляемых дисков Azure | Документы Microsoft"
description: "Как диски tooconvert из toomanaged неуправляемые дисков виртуальной Машины Windows с помощью PowerShell в модели развертывания диспетчера ресурсов hello"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Преобразование виртуальной машины Windows с неуправляемой дисков toomanaged дисков

При наличии существующих виртуальных машинах (ВМ), использующих неуправляемые диски можно преобразовать hello дисков toouse управляемых виртуальных машин через hello [управляемых дисков Azure](managed-disks-overview.md) службы. Этот процесс преобразует диска hello операционной системы и все подключенные диски данных.

В этой статье показано, как tooconvert виртуальных машин с помощью Azure PowerShell. Если необходима tooinstall или обновить ее, см. раздел [Установка и настройка Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Перед началом работы


* Просмотрите [план миграции hello дисков tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a>Преобразование одноэкземплярных виртуальных машин
В этом разделе описывается, как диски toomanaged в tooconvert экземпляра ВМ Azure из неуправляемого. (Если виртуальные машины в наборе доступности, см. следующий раздел hello.) 

1. Освободить hello виртуальной Машины с помощью hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) командлета. Hello следующий пример отменяет выделение hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`: 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. Преобразовать диски toomanaged hello ВМ с помощью hello [ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) командлета. После процесса преобразует Hello hello предыдущих виртуальной Машины, включая диск hello ОС и дисков данных:

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. Запустите hello виртуальной Машины после hello преобразования toomanaged диски с помощью [AzureRmVM начала](/powershell/module/azurerm.compute/start-azurermvm). Следующий пример перезапускается Hello hello предыдущих виртуальной Машины:

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a>Преобразование виртуальных машин в группе доступности

Если hello ВМ, которые вы хотите tooconvert toomanaged диски находятся в наборе доступности, необходимо сначала управляемый набор tooa tooconvert hello доступности группы доступности.

1. Преобразовать hello доступности с помощью hello [AzureRmAvailabilitySet обновление](/powershell/module/azurerm.compute/update-azurermavailabilityset) командлета. Следующий пример обновления hello именованный набор доступности Hello `myAvailabilitySet` в группе ресурсов hello с именем `myResourceGroup`:

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  Если hello регион, где находится в набор доступности содержит только двух доменов сбоя управляемого но hello количество доменов сбоя неуправляемые 3, эта команда отображает ошибку аналогичные слишком «hello указано число доменов сбоя 3 должно попадать в диапазон 1 too2 hello.» tooresolve hello ошибок, too2 домена сбоя hello обновления и обновления `Sku` слишком`Aligned` следующим образом:

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. Выделение и преобразовать hello виртуальных машин в группе доступности hello. Hello следующий скрипт освобождает каждой виртуальной Машины с помощью hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) , преобразует его с помощью [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)и перезапускает ее с помощью [AzureRmVM начала ](/powershell/module/azurerm.compute/start-azurermvm):

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a>Устранение неполадок

Если возникает ошибка во время преобразования, или виртуальная машина находится в состоянии сбоя из-за проблем во время предыдущего преобразования, выполнить hello `ConvertTo-AzureRmVMManagedDisk` командлет еще раз. Простой повтора обычно разблокирует hello ситуации.


## <a name="next-steps"></a>Дальнейшие действия

[Преобразуйте стандартные диски управляемого toopremium](convert-disk-storage.md)

Создайте копию виртуальной машины, доступную только для чтения, с помощью [моментальных снимков](snapshot-copy-managed-disk.md).

