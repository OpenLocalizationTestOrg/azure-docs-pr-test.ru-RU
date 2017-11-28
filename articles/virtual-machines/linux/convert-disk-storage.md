---
title: "Преобразование хранилища управляемых дисков Azure с уровня \"Стандартный\" до уровня \"Премиум\" и наоборот | Документация Майкрософт"
description: "Преобразование хранилища управляемых дисков Azure с уровня \"Стандартный\" до уровня \"Премиум\" и наоборот с помощью интерфейса командной строки Azure."
services: virtual-machines-linux
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 0380b4aaa23b4aaba4c67d05e2d62f3ef41d6a32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="e1c0d-103">Преобразование хранилища управляемых дисков Azure с уровня "Стандартный" до уровня "Премиум" и наоборот</span><span class="sxs-lookup"><span data-stu-id="e1c0d-103">Convert Azure managed disks storage from standard to premium, and vice versa</span></span>

<span data-ttu-id="e1c0d-104">Для компонента "Управляемые диски" доступны два варианта хранилища: уровень [Премиум](../../storage/storage-premium-storage.md) (на базе SSD) и уровень [Стандартный](../../storage/storage-standard-storage.md) (на базе жестких дисков).</span><span class="sxs-lookup"><span data-stu-id="e1c0d-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="e1c0d-105">Это позволяет с легкостью переключаться между двумя вариантами использования при минимальном времени простоя в зависимости от потребностей производительности.</span><span class="sxs-lookup"><span data-stu-id="e1c0d-105">It allows you to easily switch between the two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="e1c0d-106">Эта возможность недоступна для неуправляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="e1c0d-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="e1c0d-107">Но вы можете [преобразовать диски в управляемые](convert-unmanaged-to-managed-disks.md), чтобы с легкостью переключаться между двумя вариантами использования.</span><span class="sxs-lookup"><span data-stu-id="e1c0d-107">But you can easily [convert to managed disks](convert-unmanaged-to-managed-disks.md) to easily switch between the two options.</span></span>

<span data-ttu-id="e1c0d-108">В этой статье рассматривается преобразование хранилища управляемых дисков с уровня "Стандартный" до уровня "Премиум" и наоборот с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c0d-108">This article shows you how to convert managed disks from standard to premium, and vice versa by using Azure CLI.</span></span> <span data-ttu-id="e1c0d-109">Если вам установить или обновить Azure CLI, ознакомьтесь со статьей [Установка Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e1c0d-109">If you need to install or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="e1c0d-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e1c0d-110">Before you begin</span></span>

* <span data-ttu-id="e1c0d-111">Процесс преобразования требует перезагрузки виртуальной машины, поэтому запланируйте перенос хранилища дисков на предварительно установленный период обслуживания.</span><span class="sxs-lookup"><span data-stu-id="e1c0d-111">The conversion requires a restart of the VM, so schedule the migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="e1c0d-112">При использовании неуправляемых дисков сначала [преобразуйте их в управляемые диски](convert-unmanaged-to-managed-disks.md), чтобы воспользоваться приведенными в этой статье сведениями о переключении между двумя вариантами хранения.</span><span class="sxs-lookup"><span data-stu-id="e1c0d-112">If you are using unmanaged disks, first [convert to managed disks](convert-unmanaged-to-managed-disks.md) to use this article to switch between the two storage options.</span></span> 


## <a name="convert-all-the-managed-disks-of-a-vm-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="e1c0d-113">Преобразование всех управляемых дисков на виртуальной машине с уровня "Стандартный" до уровня "Премиум" и наоборот</span><span class="sxs-lookup"><span data-stu-id="e1c0d-113">Convert all the managed disks of a VM from standard to premium, and vice versa</span></span>

<span data-ttu-id="e1c0d-114">В следующем примере показано, как переключить все диски на виртуальной машине с хранилища уровня "Стандартный" на хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="e1c0d-114">In the following example, we show how to switch all the disks of a VM from standard to premium storage.</span></span> <span data-ttu-id="e1c0d-115">Чтобы использовать управляемые диски уровня "Премиум", необходимо использовать [размер виртуальной машины](sizes.md), поддерживающий хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="e1c0d-115">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="e1c0d-116">В этом примере также выполняется переключение на размер, поддерживающий хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="e1c0d-116">This example also switches to a size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains the virtual machine
rgName='yourResourceGroup'

#Name of the virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard to premium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate the VM before changing the size of the VM
az vm deallocate --name $vmName --resource-group $rgName

#Change the VM size to a size that supports premium storage 
#Skip this step if converting storage from premium to standard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update the sku of all the data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update the sku of the OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="e1c0d-117">Преобразование управляемого диска с уровня "Стандартный" до уровня "Премиум" и наоборот</span><span class="sxs-lookup"><span data-stu-id="e1c0d-117">Convert a managed disk from standard to premium, and vice versa</span></span>

<span data-ttu-id="e1c0d-118">Для среды разработки и тестирования может потребоваться сочетание дисков уровней "Стандартный" и "Премиум", чтобы сократить затраты.</span><span class="sxs-lookup"><span data-stu-id="e1c0d-118">For your dev/test workload, you may want to have mixture of standard and premium disks to reduce your cost.</span></span> <span data-ttu-id="e1c0d-119">Для этого переведите на уровень "Премиум" только диски, для которых требуется более высокая производительность.</span><span class="sxs-lookup"><span data-stu-id="e1c0d-119">You can accomplish it by upgrading to premium storage, only the disks that require better performance.</span></span> <span data-ttu-id="e1c0d-120">В следующем примере показано, как переключить диск на виртуальной машине с хранилища уровня "Стандартный" на хранилище уровня "Премиум" и наоборот.</span><span class="sxs-lookup"><span data-stu-id="e1c0d-120">In the following example, we show how to switch a single disk of a VM from standard to premium storage, and vice versa.</span></span> <span data-ttu-id="e1c0d-121">Чтобы использовать управляемые диски уровня "Премиум", необходимо использовать [размер виртуальной машины](sizes.md), поддерживающий хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="e1c0d-121">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="e1c0d-122">В этом примере также выполняется переключение на размер, поддерживающий хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="e1c0d-122">This example also switches to a size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains the managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard to premium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get the parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate the VM before changing the size of the VM
az vm deallocate --ids $vmId 

#Change the VM size to a size that supports premium storage 
#Skip this step if converting storage from premium to standard
az vm resize --ids $vmId --size $size

# Update the sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a><span data-ttu-id="e1c0d-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1c0d-123">Next steps</span></span>

<span data-ttu-id="e1c0d-124">Создайте копию виртуальной машины, доступную только для чтения, с помощью [моментальных снимков](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="e1c0d-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

