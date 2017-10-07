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
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="189f9-103">Преобразование виртуальной машины Windows с неуправляемой дисков toomanaged дисков</span><span class="sxs-lookup"><span data-stu-id="189f9-103">Convert a Windows virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="189f9-104">При наличии существующих виртуальных машинах (ВМ), использующих неуправляемые диски можно преобразовать hello дисков toouse управляемых виртуальных машин через hello [управляемых дисков Azure](managed-disks-overview.md) службы.</span><span class="sxs-lookup"><span data-stu-id="189f9-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="189f9-105">Этот процесс преобразует диска hello операционной системы и все подключенные диски данных.</span><span class="sxs-lookup"><span data-stu-id="189f9-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="189f9-106">В этой статье показано, как tooconvert виртуальных машин с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="189f9-106">This article shows you how tooconvert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="189f9-107">Если необходима tooinstall или обновить ее, см. раздел [Установка и настройка Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="189f9-107">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="189f9-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="189f9-108">Before you begin</span></span>


* <span data-ttu-id="189f9-109">Просмотрите [план миграции hello дисков tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="189f9-109">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="189f9-110">Преобразование одноэкземплярных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="189f9-110">Convert single-instance VMs</span></span>
<span data-ttu-id="189f9-111">В этом разделе описывается, как диски toomanaged в tooconvert экземпляра ВМ Azure из неуправляемого.</span><span class="sxs-lookup"><span data-stu-id="189f9-111">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="189f9-112">(Если виртуальные машины в наборе доступности, см. следующий раздел hello.)</span><span class="sxs-lookup"><span data-stu-id="189f9-112">(If your VMs are in an availability set, see hello next section.)</span></span> 

1. <span data-ttu-id="189f9-113">Освободить hello виртуальной Машины с помощью hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) командлета.</span><span class="sxs-lookup"><span data-stu-id="189f9-113">Deallocate hello VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="189f9-114">Hello следующий пример отменяет выделение hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="189f9-114">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="189f9-115">Преобразовать диски toomanaged hello ВМ с помощью hello [ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) командлета.</span><span class="sxs-lookup"><span data-stu-id="189f9-115">Convert hello VM toomanaged disks by using hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="189f9-116">После процесса преобразует Hello hello предыдущих виртуальной Машины, включая диск hello ОС и дисков данных:</span><span class="sxs-lookup"><span data-stu-id="189f9-116">hello following process converts hello previous VM, including hello OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="189f9-117">Запустите hello виртуальной Машины после hello преобразования toomanaged диски с помощью [AzureRmVM начала](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="189f9-117">Start hello VM after hello conversion toomanaged disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="189f9-118">Следующий пример перезапускается Hello hello предыдущих виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="189f9-118">hello following example restarts hello previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="189f9-119">Преобразование виртуальных машин в группе доступности</span><span class="sxs-lookup"><span data-stu-id="189f9-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="189f9-120">Если hello ВМ, которые вы хотите tooconvert toomanaged диски находятся в наборе доступности, необходимо сначала управляемый набор tooa tooconvert hello доступности группы доступности.</span><span class="sxs-lookup"><span data-stu-id="189f9-120">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

1. <span data-ttu-id="189f9-121">Преобразовать hello доступности с помощью hello [AzureRmAvailabilitySet обновление](/powershell/module/azurerm.compute/update-azurermavailabilityset) командлета.</span><span class="sxs-lookup"><span data-stu-id="189f9-121">Convert hello availability set by using hello [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="189f9-122">Следующий пример обновления hello именованный набор доступности Hello `myAvailabilitySet` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="189f9-122">hello following example updates hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="189f9-123">Если hello регион, где находится в набор доступности содержит только двух доменов сбоя управляемого но hello количество доменов сбоя неуправляемые 3, эта команда отображает ошибку аналогичные слишком «hello указано число доменов сбоя 3 должно попадать в диапазон 1 too2 hello.»</span><span class="sxs-lookup"><span data-stu-id="189f9-123">If hello region where your availability set is located has only 2 managed fault domains but hello number of unmanaged fault domains is 3, this command shows an error similar too"hello specified fault domain count 3 must fall in hello range 1 too2."</span></span> <span data-ttu-id="189f9-124">tooresolve hello ошибок, too2 домена сбоя hello обновления и обновления `Sku` слишком`Aligned` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="189f9-124">tooresolve hello error, update hello fault domain too2 and update `Sku` too`Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="189f9-125">Выделение и преобразовать hello виртуальных машин в группе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="189f9-125">Deallocate and convert hello VMs in hello availability set.</span></span> <span data-ttu-id="189f9-126">Hello следующий скрипт освобождает каждой виртуальной Машины с помощью hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) , преобразует его с помощью [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)и перезапускает ее с помощью [AzureRmVM начала ](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="189f9-126">hello following script deallocates each VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

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


## <a name="troubleshooting"></a><span data-ttu-id="189f9-127">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="189f9-127">Troubleshooting</span></span>

<span data-ttu-id="189f9-128">Если возникает ошибка во время преобразования, или виртуальная машина находится в состоянии сбоя из-за проблем во время предыдущего преобразования, выполнить hello `ConvertTo-AzureRmVMManagedDisk` командлет еще раз.</span><span class="sxs-lookup"><span data-stu-id="189f9-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run hello `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="189f9-129">Простой повтора обычно разблокирует hello ситуации.</span><span class="sxs-lookup"><span data-stu-id="189f9-129">A simple retry usually unblocks hello situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="189f9-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="189f9-130">Next steps</span></span>

[<span data-ttu-id="189f9-131">Преобразуйте стандартные диски управляемого toopremium</span><span class="sxs-lookup"><span data-stu-id="189f9-131">Convert standard managed disks toopremium</span></span>](convert-disk-storage.md)

<span data-ttu-id="189f9-132">Создайте копию виртуальной машины, доступную только для чтения, с помощью [моментальных снимков](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="189f9-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

