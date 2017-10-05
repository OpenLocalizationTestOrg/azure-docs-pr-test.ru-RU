---
title: "Управляемые диски Azure. Преобразование виртуальной машины Windows с неуправляемыми дисками для использования управляемых дисков | Документация Майкрософт"
description: "Переключение виртуальной машины Windows, развернутой в рамках модели Resource Manager, с неуправляемых дисков на управляемые диски с помощью PowerShell."
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
ms.openlocfilehash: 54afcf1e37f696979bfe270a473c72aedf20dc43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="a3cae-103">Переключение виртуальной машины Windows с неуправляемых дисков на управляемые диски</span><span class="sxs-lookup"><span data-stu-id="a3cae-103">Convert a Windows virtual machine from unmanaged disks to managed disks</span></span>

<span data-ttu-id="a3cae-104">При наличии виртуальных машин Windows, использующих неуправляемые диски, их можно преобразовать для использования управляемых дисков с помощью службы [Управляемые диски Azure](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3cae-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use managed disks through the [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="a3cae-105">При этом преобразуются диск операционной системы и все подключенные диски данных.</span><span class="sxs-lookup"><span data-stu-id="a3cae-105">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="a3cae-106">В этой статье показано, как преобразовать виртуальные машины с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3cae-106">This article shows you how to convert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="a3cae-107">Если вам необходимо установить или обновить Azure PowerShell, ознакомьтесь со статьей [об установке и настройке Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a3cae-107">If you need to install or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a3cae-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a3cae-108">Before you begin</span></span>


* <span data-ttu-id="a3cae-109">Просмотрите раздел [Планирование миграции на управляемые диски](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="a3cae-109">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="a3cae-110">Преобразование одноэкземплярных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="a3cae-110">Convert single-instance VMs</span></span>
<span data-ttu-id="a3cae-111">В этом разделе описывается, как преобразовать одноэкземплярные виртуальные машины Azure с неуправляемыми дисками, чтобы они могли использовать Управляемые диски.</span><span class="sxs-lookup"><span data-stu-id="a3cae-111">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="a3cae-112">(Если виртуальные машины находятся в группе доступности, ознакомьтесь со следующим разделом.)</span><span class="sxs-lookup"><span data-stu-id="a3cae-112">(If your VMs are in an availability set, see the next section.)</span></span> 

1. <span data-ttu-id="a3cae-113">Отмените выделение виртуальной машины с помощью командлета [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="a3cae-113">Deallocate the VM by using the [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="a3cae-114">В следующем примере освобождается виртуальная машина `myVM`, входящая в группу ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="a3cae-114">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="a3cae-115">Преобразуйте виртуальную машину для использования управляемых дисков с помощью командлета [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk).</span><span class="sxs-lookup"><span data-stu-id="a3cae-115">Convert the VM to managed disks by using the [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="a3cae-116">Приведенный ниже процесс преобразовывает виртуальную машину, включая ее диск ОС и все диски данных.</span><span class="sxs-lookup"><span data-stu-id="a3cae-116">The following process converts the previous VM, including the OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="a3cae-117">После преобразования запустите виртуальную машину с помощью командлета [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="a3cae-117">Start the VM after the conversion to managed disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="a3cae-118">Следующий пример перезапустит предыдущую виртуальную машину:</span><span class="sxs-lookup"><span data-stu-id="a3cae-118">The following example restarts the previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="a3cae-119">Преобразование виртуальных машин в группе доступности</span><span class="sxs-lookup"><span data-stu-id="a3cae-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="a3cae-120">Если виртуальные машины, которые вы хотите преобразовать для использования управляемых дисков, входят в группу доступности, то необходимо сначала преобразовать эту группу доступности в управляемую группу доступности.</span><span class="sxs-lookup"><span data-stu-id="a3cae-120">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

1. <span data-ttu-id="a3cae-121">Преобразуйте группу доступности с помощью командлета [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="a3cae-121">Convert the availability set by using the [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="a3cae-122">В следующем примере преобразовывается группа доступности `myAvailabilitySet` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="a3cae-122">The following example updates the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="a3cae-123">Если регион, в котором находится группа доступности, имеет только 2 управляемых домена сбоя, но количество неуправляемых доменов сбоя равно 3, отобразится ошибка "Указанное число доменов сбоя 3 должно быть в диапазоне от 1 до 2".</span><span class="sxs-lookup"><span data-stu-id="a3cae-123">If the region where your availability set is located has only 2 managed fault domains but the number of unmanaged fault domains is 3, this command shows an error similar to "The specified fault domain count 3 must fall in the range 1 to 2."</span></span> <span data-ttu-id="a3cae-124">Чтобы устранить эту ошибку, необходимо обновить количество доменов сбоя до двух и обновить значение `Sku` к `Aligned` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a3cae-124">To resolve the error, update the fault domain to 2 and update `Sku` to `Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="a3cae-125">Освободите и преобразуйте виртуальные машины в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="a3cae-125">Deallocate and convert the VMs in the availability set.</span></span> <span data-ttu-id="a3cae-126">Следующий сценарий отменяет выделение каждой виртуальной машины с помощью командлета [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm), а затем преобразует ее с помощью командлета [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) и перезапускает с помощью командлета [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="a3cae-126">The following script deallocates each VM by using the [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

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


## <a name="troubleshooting"></a><span data-ttu-id="a3cae-127">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="a3cae-127">Troubleshooting</span></span>

<span data-ttu-id="a3cae-128">Если во время преобразования произойдет ошибка или виртуальная машина находится в состоянии сбоя из-за проблем во время предыдущего преобразования, выполните командлет `ConvertTo-AzureRmVMManagedDisk` еще раз.</span><span class="sxs-lookup"><span data-stu-id="a3cae-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run the `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="a3cae-129">Простой повтор обычно решает проблему.</span><span class="sxs-lookup"><span data-stu-id="a3cae-129">A simple retry usually unblocks the situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a3cae-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3cae-130">Next steps</span></span>

[<span data-ttu-id="a3cae-131">Преобразование управляемых дисков уровня "Стандартный" в диски уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="a3cae-131">Convert standard managed disks to premium</span></span>](convert-disk-storage.md)

<span data-ttu-id="a3cae-132">Создайте копию виртуальной машины, доступную только для чтения, с помощью [моментальных снимков](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="a3cae-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

