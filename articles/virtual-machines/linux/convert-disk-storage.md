---
title: "aaaConvert Azure управлять дисками из стандартных toopremium и наоборот | Документы Microsoft"
description: "Как tooconvert Azure Управление дисками из стандартных toopremium и наоборот, с помощью Azure CLI."
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
ms.openlocfilehash: 261d77202f7fd381085c4e25211a5d0026f43b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="c57f6-103">Преобразовать Azure управлять дисками из стандартных toopremium и наоборот</span><span class="sxs-lookup"><span data-stu-id="c57f6-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="c57f6-104">Для компонента "Управляемые диски" доступны два варианта хранилища: уровень [Премиум](../../storage/storage-premium-storage.md) (на базе SSD) и уровень [Стандартный](../../storage/storage-standard-storage.md) (на базе жестких дисков).</span><span class="sxs-lookup"><span data-stu-id="c57f6-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="c57f6-105">Она позволяет tooeasily переключение между hello двух параметров с минимальным временем простоя, зависимости от потребностей производительности.</span><span class="sxs-lookup"><span data-stu-id="c57f6-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="c57f6-106">Эта возможность недоступна для неуправляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="c57f6-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="c57f6-107">Но вы можете легко [преобразования дисков toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily переключение между hello двух параметров.</span><span class="sxs-lookup"><span data-stu-id="c57f6-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="c57f6-108">В этой статье показано, как управление tooconvert диски из стандартных toopremium и обратно с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c57f6-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure CLI.</span></span> <span data-ttu-id="c57f6-109">Если необходима tooinstall или обновить ее, см. раздел [установить CLI Azure 2.0](/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c57f6-109">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="c57f6-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="c57f6-110">Before you begin</span></span>

* <span data-ttu-id="c57f6-111">требуется для преобразования Hello hello виртуальной Машины, таким образом график миграции hello дисков хранилища во время периода обслуживания существующих.</span><span class="sxs-lookup"><span data-stu-id="c57f6-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="c57f6-112">При использовании неуправляемого диски сначала [преобразования дисков toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch этой статье между hello двух вариантов хранения.</span><span class="sxs-lookup"><span data-stu-id="c57f6-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="c57f6-113">Преобразовать все hello управляемых дисков виртуальной машины из стандартных toopremium и наоборот</span><span class="sxs-lookup"><span data-stu-id="c57f6-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="c57f6-114">В следующем примере hello, показано, как tooswitch все hello дисков виртуальной машины из стандартных toopremium хранилища.</span><span class="sxs-lookup"><span data-stu-id="c57f6-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="c57f6-115">toouse premium управляемых дисков, необходимо использовать ВМ [размер виртуальной Машины](sizes.md) с поддержкой хранилище premium.</span><span class="sxs-lookup"><span data-stu-id="c57f6-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="c57f6-116">В этом примере также переключает tooa размер, который поддерживает хранилище premium.</span><span class="sxs-lookup"><span data-stu-id="c57f6-116">This example also switches tooa size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains hello virtual machine
rgName='yourResourceGroup'

#Name of hello virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --name $vmName --resource-group $rgName

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update hello sku of all hello data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update hello sku of hello OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="c57f6-117">Преобразовать управляемого диска из стандартных toopremium и наоборот</span><span class="sxs-lookup"><span data-stu-id="c57f6-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="c57f6-118">Для рабочей нагрузки для разработки и тестирования вы можете toohave сочетание tooreduce диски standard и premium затрат.</span><span class="sxs-lookup"><span data-stu-id="c57f6-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="c57f6-119">Его можно выполнить после обновления хранилища toopremium только диски hello, требующих более высокую производительность.</span><span class="sxs-lookup"><span data-stu-id="c57f6-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="c57f6-120">В следующем примере hello, показано, как tooswitch одного диска виртуальной машины из стандартных toopremium хранилища и наоборот.</span><span class="sxs-lookup"><span data-stu-id="c57f6-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="c57f6-121">toouse premium управляемых дисков, необходимо использовать ВМ [размер виртуальной Машины](sizes.md) с поддержкой хранилище premium.</span><span class="sxs-lookup"><span data-stu-id="c57f6-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="c57f6-122">В этом примере также переключает tooa размер, который поддерживает хранилище premium.</span><span class="sxs-lookup"><span data-stu-id="c57f6-122">This example also switches tooa size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains hello managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get hello parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --ids $vmId 

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --ids $vmId --size $size

# Update hello sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a><span data-ttu-id="c57f6-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c57f6-123">Next steps</span></span>

<span data-ttu-id="c57f6-124">Создайте копию виртуальной машины, доступную только для чтения, с помощью [моментальных снимков](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="c57f6-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

