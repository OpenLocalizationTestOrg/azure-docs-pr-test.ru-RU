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
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Преобразовать Azure управлять дисками из стандартных toopremium и наоборот

Для компонента "Управляемые диски" доступны два варианта хранилища: уровень [Премиум](../../storage/storage-premium-storage.md) (на базе SSD) и уровень [Стандартный](../../storage/storage-standard-storage.md) (на базе жестких дисков). Она позволяет tooeasily переключение между hello двух параметров с минимальным временем простоя, зависимости от потребностей производительности. Эта возможность недоступна для неуправляемых дисков. Но вы можете легко [преобразования дисков toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily переключение между hello двух параметров.

В этой статье показано, как управление tooconvert диски из стандартных toopremium и обратно с помощью Azure CLI. Если необходима tooinstall или обновить ее, см. раздел [установить CLI Azure 2.0](/cli/azure/install-azure-cli.md). 

## <a name="before-you-begin"></a>Перед началом работы

* требуется для преобразования Hello hello виртуальной Машины, таким образом график миграции hello дисков хранилища во время периода обслуживания существующих. 
* При использовании неуправляемого диски сначала [преобразования дисков toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch этой статье между hello двух вариантов хранения. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Преобразовать все hello управляемых дисков виртуальной машины из стандартных toopremium и наоборот

В следующем примере hello, показано, как tooswitch все hello дисков виртуальной машины из стандартных toopremium хранилища. toouse premium управляемых дисков, необходимо использовать ВМ [размер виртуальной Машины](sizes.md) с поддержкой хранилище premium. В этом примере также переключает tooa размер, который поддерживает хранилище premium.

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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Преобразовать управляемого диска из стандартных toopremium и наоборот

Для рабочей нагрузки для разработки и тестирования вы можете toohave сочетание tooreduce диски standard и premium затрат. Его можно выполнить после обновления хранилища toopremium только диски hello, требующих более высокую производительность. В следующем примере hello, показано, как tooswitch одного диска виртуальной машины из стандартных toopremium хранилища и наоборот. toouse premium управляемых дисков, необходимо использовать ВМ [размер виртуальной Машины](sizes.md) с поддержкой хранилище premium. В этом примере также переключает tooa размер, который поддерживает хранилище premium.

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

## <a name="next-steps"></a>Дальнейшие действия

Создайте копию виртуальной машины, доступную только для чтения, с помощью [моментальных снимков](snapshot-copy-managed-disk.md).

