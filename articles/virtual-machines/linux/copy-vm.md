---
title: "Виртуальная машина Linux с помощью Azure CLI 2.0 aaaCopy | Документы Microsoft"
description: "Узнайте, как toocreate копию ВМ Linux Azure с помощью Azure CLI 2.0 и управляемых дисков."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a>Создание копии виртуальной машины Linux с помощью Azure CLI 2.0 и Управляемых дисков


В этой статье показано, как hello toocreate копии Azure виртуальной машины (VM) под управлением Linux с помощью Azure CLI 2.0 и модель развертывания диспетчера ресурсов Azure hello. Можно также выполнить следующие действия с hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Кроме того, можно [передать VHD и создать виртуальную машину на его основе](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Предварительные требования


-   Установка [Azure CLI 2.0](/cli/azure/install-az-cli2)

-   Войдите в tooan учетная запись Azure с [входа az](/cli/azure/#login).

-   Иметь toouse виртуальной Машины Azure в качестве hello источником для копии.

## <a name="step-1-stop-hello-source-vm"></a>Шаг 1: Остановите hello исходной виртуальной Машины


Освободить hello исходной виртуальной Машины с помощью [ВМ az deallocate](/cli/azure/vm#deallocate).
Hello следующий пример отменяет выделение hello виртуальной Машины с именем **myVM** в группе ресурсов hello **myResourceGroup**:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a>Шаг 2: Скопируйте hello исходной виртуальной Машины


toocopy виртуальной Машины, можно создать копию hello базового виртуального жесткого диска. Этот процесс создает специализированные виртуального жесткого диска в качестве управляемого диска, содержащего hello одинаковые конфигурации и параметры, как hello исходной виртуальной Машины.

Дополнительные сведения об Управляемых дисках Azure см. в [обзоре Управляемых дисков Azure](../windows/managed-disks-overview.md). 

1.  Все имена виртуальных Машин и hello его диска операционной системы с [список виртуальных машин az](/cli/azure/vm#list). Hello следующий пример отображает список всех виртуальных машин в группе ресурсов с именем **myResourceGroup**:
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    Hello вывода будет примерно toohello следующий пример:

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  Копировать диск hello путем создания нового управляемого диска с помощью [создать диск az](/cli/azure/disk#create). Hello следующий пример создает диск с именем **myCopiedDisk** из hello управляемым диск с именем **myDisk**:

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  Проверьте диски hello управляемых теперь в группе ресурсов с помощью [список дисков az](/cli/azure/disk#list). Hello в примере список управляемых hello дисков в группе ресурсов hello с именем **myResourceGroup**:

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  Пропустить слишком[«шаг 3: Настройка виртуальной сети»](#step-3-set-up-a-virtual-network).


## <a name="step-3-set-up-a-virtual-network"></a>Шаг 3. Настройка виртуальной сети


Hello следующих дополнительных шагов создания новой виртуальной сети, подсети, общедоступный IP-адрес и виртуальный сетевой адаптер (NIC).

При копировании виртуальной Машины для устранения неполадок или дополнительные развертывания, вы можете не toouse виртуальной Машины в существующей виртуальной сети.

Если требуется toocreate инфраструктуре виртуальной сети для виртуальных машин скопированный выполните рядом hello несколько действий. Если вы не хотите toocreate виртуальную сеть, пропустите слишком[шаг 4: создайте виртуальную Машину](#step-4-create-a-vm).

1.  Создайте виртуальную сеть hello с помощью [создания az сети vnet](/cli/azure/network/vnet#create). Hello следующий пример создает виртуальную сеть с именем **myVnet** и подсеть с именем **mySubnet**:

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  Создайте общедоступный IP-адрес, выполнив команду [az network public-ip create](/cli/azure/network/public-ip#create). Hello следующий пример создает общедоступный IP-адрес с именем **myPublicIP** с именем DNS hello **mypublicdns**. (hello DNS-имя должно быть уникальным, поэтому введите уникальное имя).

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  Создание с помощью Сетевых hello [Создание сетевого адаптера сети az](/cli/azure/network/nic#create).
    Hello следующий пример создает сетевой Адаптер с именем **myNic** с присоединенного toothe **mySubnet** подсети:

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a>Шаг 4. Создание виртуальной машины

Теперь можно создать виртуальную машину, выполнив команду [az vm create](/cli/azure/vm#create).

Указать hello Копировать toouse управляемого диск как диск ОС hello (--присоединить os диск), как показано ниже:

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a>Дальнейшие действия

toolearn как toomanage Azure CLI toouse новых виртуальных Машин, в разделе [команды Azure CLI для диспетчера ресурсов Azure hello](../azure-cli-arm-commands.md).
