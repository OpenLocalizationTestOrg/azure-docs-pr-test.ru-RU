---
title: "aaaDetach диск данных от виртуальной Машины Windows - Azure | Документы Microsoft"
description: "Узнайте, toodetach диск данных от виртуальной машины в Azure с помощью модели развертывания диспетчера ресурсов hello."
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
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="6d4eb-103">Toodetach данных места на диске из виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="6d4eb-103">How toodetach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="6d4eb-104">Если диск данных, вложенные tooa виртуальной машины больше не нужен, можно легко отключить ее.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="6d4eb-105">Удаляет диск hello из hello виртуальной машины, но не удаляет его из хранилища.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="6d4eb-106">Если отключить диск, он не удаляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="6d4eb-107">Если вы подписаны tooPremium хранилища, снова tooincur плата хранения для диска hello.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="6d4eb-108">Дополнительные сведения см. в разделе слишком[цены и выставление счетов при использовании хранилища Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="6d4eb-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="6d4eb-109">Если требуется toouse hello существующие данные на диске hello, вам может быть повторно присоединена toohello одной виртуальной машине, так и любой другой.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="6d4eb-110">Отсоединить диск данных с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="6d4eb-110">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="6d4eb-111">В концентраторе hello портала выберите **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-111">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="6d4eb-112">Выберите hello виртуальную машину с диска данных hello toodetach и щелкните **остановить** toodeallocate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-112">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="6d4eb-113">В колонке hello виртуальной машины, выберите **дисков**.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-113">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="6d4eb-114">Вверху hello hello **дисков** колонке выберите **изменить**.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-114">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="6d4eb-115">В hello **дисков** колонке toohello правому краю hello диск данных, что хотелось бы toodetach, щелкните hello ![изображение кнопки отсоединения](./media/detach-disk/detach.png) «отсоединить».</span><span class="sxs-lookup"><span data-stu-id="6d4eb-115">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="6d4eb-116">После удаления диска hello щелкните Сохранить hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-116">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="6d4eb-117">В колонке hello виртуальную машину, щелкните **Обзор** и нажмите кнопку hello **запустить** кнопку вверху hello hello toorestart hello колонке виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-117">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>



<span data-ttu-id="6d4eb-118">Hello диск остается в хранилище, но больше не tooa подключенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-118">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="6d4eb-119">Отключение диска данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d4eb-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="6d4eb-120">В этом примере hello первая команда получает hello виртуальной машины с именем **MyVM07** в hello **RG11** группы ресурсов с помощью командлета Get-AzureRmVM hello.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-120">In this example, hello first command gets hello virtual machine named **MyVM07** in hello **RG11** resource group using hello Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="6d4eb-121">Здравствуйте, команда сохраняет hello виртуальной машины в hello **$VirtualMachine** переменной.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-121">hello command stores hello virtual machine in hello **$VirtualMachine** variable.</span></span>

<span data-ttu-id="6d4eb-122">Вторая команда Hello удаляет hello диск данных, с именем DataDisk3 из hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-122">hello second command removes hello data disk named DataDisk3 from hello virtual machine.</span></span>

<span data-ttu-id="6d4eb-123">Последняя команда Hello обновляет состояние hello для hello виртуальной машины toocomplete hello процесс удаления диска данных hello.</span><span class="sxs-lookup"><span data-stu-id="6d4eb-123">hello final command updates hello state of hello virtual machine toocomplete hello process of removing hello data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="6d4eb-124">Дополнительные сведения см. в разделе [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="6d4eb-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d4eb-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d4eb-125">Next steps</span></span>
<span data-ttu-id="6d4eb-126">Если требуется диск данных tooreuse hello, только что [присоединить ее tooanother виртуальной Машины](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6d4eb-126">If you want tooreuse hello data disk, you can just [attach it tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

