---
title: "aaaCreate управляемого диска из VHD в Azure | Документы Microsoft"
description: "Создание управляемого диска из VHD, который в данный момент учетной записью хранения Azure с помощью модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="b50da-103">Создание управляемых дисков из неуправляемых дисков в учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="b50da-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="b50da-104">Управляемый диск можно создать из существующего диска данных или диска ОС, который в данный момент находится в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b50da-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="b50da-105">Вы также можете создавать пустой диск, который можно использовать в качестве нового диска данных для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b50da-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="b50da-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="b50da-106">Before you begin</span></span>
<span data-ttu-id="b50da-107">При использовании PowerShell убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="b50da-107">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="b50da-108">Запустите hello следующие tooinstall команды.</span><span class="sxs-lookup"><span data-stu-id="b50da-108">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="b50da-109">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b50da-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="b50da-110">Создание управляемого диска из виртуального жесткого диска в учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="b50da-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="b50da-111">В примере hello мы создать диск из VHD как управляемого диска и назначьте его параметр toohello **диск 1 $** toouse позже.</span><span class="sxs-lookup"><span data-stu-id="b50da-111">In hello example we create a disk from a VHD as managed disk and assign it toohello parameter **$disk1** toouse later.</span></span> 

<span data-ttu-id="b50da-112">Hello управляемого диска будет создан в hello **Запад США** расположения в группу ресурсов с именем **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="b50da-112">hello managed disk will be created in hello **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="b50da-113">Hello диск будет называться **myDisk** и он будет создан из VHD-файл с именем **myDisk.vhd** мы ранее отправленные tooa учетной записи хранилища с именем **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="b50da-113">hello disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded tooa storage account named **mystorageaccount**.</span></span> <span data-ttu-id="b50da-114">Hello управляемого диска будут созданы в premium локально избыточное хранилище (LRS).</span><span class="sxs-lookup"><span data-stu-id="b50da-114">hello managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="b50da-115">StandardLRS и PremiumLRS являются только hello **- AccountType** параметры, доступные для управляемых дисках.</span><span class="sxs-lookup"><span data-stu-id="b50da-115">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="b50da-116">Задайте некоторые параметры.</span><span class="sxs-lookup"><span data-stu-id="b50da-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="b50da-117">Создайте диск данных hello.</span><span class="sxs-lookup"><span data-stu-id="b50da-117">Create hello data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="b50da-118">Создание пустого диска данных в качестве управляемого диска</span><span class="sxs-lookup"><span data-stu-id="b50da-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="b50da-119">В примере hello мы создайте пустой диск данных как управляемого диска и назначьте его параметр toohello **$dataDisk2** toouse позже.</span><span class="sxs-lookup"><span data-stu-id="b50da-119">In hello example we create an empty data disk as managed disk and assign it toohello parameter **$dataDisk2** toouse later.</span></span> <span data-ttu-id="b50da-120">Пустой диск данных потребуется инициализировать toobe входа в toohello виртуальной Машины, с помощью diskmgmt.msc или [удаленно с помощью WinRM и сценарий](attach-disk-ps.md#initialize-the-disk), после вложенного tooa запуск виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b50da-120">An empty data disk will need toobe initialized logging in toohello VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached tooa running VM.</span></span>

<span data-ttu-id="b50da-121">Hello пустой диск данных будет создан в hello **Западная центральной части США** расположения в группу ресурсов с именем **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="b50da-121">hello empty data disk will be created in hello **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="b50da-122">Hello диск будет называться **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="b50da-122">hello disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="b50da-123">пустой диск Hello будут созданы в premium локально избыточное хранилище (LRS).</span><span class="sxs-lookup"><span data-stu-id="b50da-123">hello empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="b50da-124">StandardLRS и PremiumLRS являются только hello **- AccountType** параметры, доступные для управляемых дисках.</span><span class="sxs-lookup"><span data-stu-id="b50da-124">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="b50da-125">размер диска Hello в этом примере — 128 ГБ, но необходимо выбрать размер, который соответствует требованиям hello любые приложения, запущенные на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="b50da-125">hello disk size in this example is 128GB, but you should choose a size that meets hello needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="b50da-126">Задайте некоторые параметры.</span><span class="sxs-lookup"><span data-stu-id="b50da-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="b50da-127">Создайте диск данных hello.</span><span class="sxs-lookup"><span data-stu-id="b50da-127">Create hello data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="b50da-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b50da-128">Next Steps</span></span>   
- <span data-ttu-id="b50da-129">К имеющейся виртуальной машине можно [подключить диск данных](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b50da-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
