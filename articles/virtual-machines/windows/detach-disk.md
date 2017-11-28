---
title: "Отключение диска данных от виртуальной машины Windows в Azure | Документация Майкрософт"
description: "Узнайте, как отключить диск данных от виртуальной машины в Azure с использованием модели развертывания с помощью Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 97aa69745d200ee76f9f859eb3a8b0ad2f202bad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="4d9b3-103">Отключение диска от виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="4d9b3-103">How to detach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="4d9b3-104">Когда диск данных, подключенный к виртуальной машине, больше не нужен, его можно легко отключить.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="4d9b3-105">При данной операции происходит удаление диска из виртуальной машины, но не из хранилища.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="4d9b3-106">Если отключить диск, он не удаляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="4d9b3-107">Если вы подписаны на хранилище уровня "Премиум", с вас по-прежнему будет взиматься плата за хранение этого диска.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="4d9b3-108">Дополнительные сведения см. в разделе [Цены и выставление счетов](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="4d9b3-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="4d9b3-109">Если вы хотите снова использовать существующие данные на диске, его можно легко повторно подключить как к той же самой, так и к другой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="4d9b3-110">Отключение диска данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="4d9b3-110">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="4d9b3-111">В главном меню портала выберите **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-111">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="4d9b3-112">Выберите виртуальную машину, от которой нужно отключить диск данных, и щелкните **Остановить**, чтобы отменить ее распределение.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-112">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="4d9b3-113">В колонке "Виртуальная машина" выберите **Диски**.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-113">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="4d9b3-114">В верхней части колонки **Диски** выберите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-114">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="4d9b3-115">В колонке **Диски** справа от диска данных, который требуется отключить, нажмите кнопку ![Отключить](./media/detach-disk/detach.png).</span><span class="sxs-lookup"><span data-stu-id="4d9b3-115">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="4d9b3-116">После удаления диска в верхней части колонки нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="4d9b3-116">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="4d9b3-117">В колонке виртуальной машины щелкните **Обзор** и нажмите кнопку **Запустить** вверху, чтобы перезапустить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-117">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>



<span data-ttu-id="4d9b3-118">Диск остается в хранилище, но более не подключен к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-118">The disk remains in storage but is no longer attached to a virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="4d9b3-119">Отключение диска данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d9b3-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="4d9b3-120">В этом примере первая команда возвращает виртуальную машину **MyVM07** в группе ресурсов **RG11** с помощью командлета Get-AzureRmVM.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-120">In this example, the first command gets the virtual machine named **MyVM07** in the **RG11** resource group using the Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="4d9b3-121">Она сохраняет имя виртуальной машины в переменной **$VirtualMachine** .</span><span class="sxs-lookup"><span data-stu-id="4d9b3-121">The command stores the virtual machine in the **$VirtualMachine** variable.</span></span>

<span data-ttu-id="4d9b3-122">Вторая команда удаляет диск данных DataDisk3 из этой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-122">The second command removes the data disk named DataDisk3 from the virtual machine.</span></span>

<span data-ttu-id="4d9b3-123">Последняя команда обновляет состояние виртуальной машины, чтобы завершить процесс удаления диска данных.</span><span class="sxs-lookup"><span data-stu-id="4d9b3-123">The final command updates the state of the virtual machine to complete the process of removing the data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="4d9b3-124">Дополнительные сведения см. в разделе [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="4d9b3-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d9b3-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d9b3-125">Next steps</span></span>
<span data-ttu-id="4d9b3-126">Если вы хотите повторно использовать диск данных, то можете просто [подключить его к другой виртуальной машине](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4d9b3-126">If you want to reuse the data disk, you can just [attach it to another VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

