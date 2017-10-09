---
title: "aaaCreate виртуальной Машины Linux в Azure с несколькими сетевыми адаптерами | Документы Microsoft"
description: "Узнайте, как toocreate ВМ Linux с несколькими сетевыми адаптерами присоединенного tooit с помощью шаблонов hello Azure CLI 2.0 или диспетчер ресурсов."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>Как toocreate виртуальной машины Linux в Azure с несколькими сетевыми интерфейсные карты
Можно создать виртуальную машину (ВМ) в Azure, которая имеет несколько tooit интерфейсов (NIC), подключенных виртуальных сетей. Типичный сценарий состоит в разных подсетях toohave для внешнего и внутреннего интерфейса подключения или сеть, выделенная tooa наблюдения или решение для резервного копирования. В этой статье описаны процедуры tooit присоединенного toocreate виртуальной Машины с несколькими сетевыми адаптерами и tooadd или удаление сетевых адаптеров в существующей виртуальной Машины. Подробные сведения, включая как toocreate несколько сетевых адаптеров в собственных Bash скрипты, Дополнительные сведения о [развертывание виртуальных машин multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Различные [размеры виртуальных машин](sizes.md) поддерживают разное число сетевых карт, так что выбирайте соответствующий размер виртуальной машины.

В этой статье указаны как toocreate a виртуальной Машины с несколькими сетевыми адаптерами с hello Azure CLI 2.0. Можно также выполнить следующие действия с hello [Azure CLI 1.0](multiple-nics-nodejs.md).


## <a name="create-supporting-resources"></a>Создание вспомогательных ресурсов
Последняя версия hello установки [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.

Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:

```azurecli
az group create --name myResourceGroup --location eastus
```

Создайте виртуальную сеть hello с [создания az сети vnet](/cli/azure/network/vnet#create). Hello следующий пример создает виртуальную сеть с именем *myVnet* и подсеть с именем *mySubnetFrontEnd*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

Создайте подсеть для трафика hello серверной части с [создать подсеть виртуальной сети az сети](/cli/azure/network/vnet/subnet#create). Hello следующий пример создает подсеть с именем *mySubnetBackEnd*:

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

Создайте группу безопасности сети с помощью команды [az network nsg create](/cli/azure/network/nsg#create). Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>Создание и настройка нескольких сетевых карт
Создайте две сетевых карты с помощью команды [az network nic create](/cli/azure/network/nic#create). Hello следующий пример создает два сетевых адаптера с именем *myNic1* и *myNic2*, подключенной группы безопасности сети hello с одним сетевым Адаптером подключение tooeach подсети:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Создайте виртуальную Машину и присоединения hello сетевых адаптеров
При создании hello виртуальных Машин, укажите hello сетевые адаптеры, созданные с помощью `--nics`. Необходимо также tootake осторожность при выборе hello размер виртуальной Машины. Существуют ограничения для hello общее число сетевых адаптеров, вы можете добавить tooa виртуальной Машины. Прочитайте дополнительные сведения о [размерах виртуальных машин Linux](sizes.md). 

Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). Hello следующий пример создает Виртуальную машину с именем *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a>Добавить tooa сетевого Адаптера виртуальной Машины
Hello предыдущие шаги создания виртуальной Машины с несколькими сетевыми адаптерами. Можно также добавить существующие ВМ в Azure CLI 2.0 hello tooan сетевых адаптеров. 

Создайте другую сетевую карту с помощью команды [az network nic create](/cli/azure/network/nic#create). Hello следующий пример создает сетевой Адаптер с именем *myNic3* подключен toohello внутренней подсети и сетевой группы безопасности, созданные в предыдущих шагах hello:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

tooadd tooan Сетевых существующую виртуальную Машину сначала освободить hello виртуальной Машины с [deallocate az ВМ](/cli/azure/vm#deallocate). Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Добавить hello сетевого Адаптера с [добавить сетевой адаптер виртуальной машины az](/cli/azure/vm/nic#add). Hello следующий пример добавляет *myNic3* слишком*myVM*:

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

Запуск hello виртуальной Машины с [запуска виртуальной машины az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>Удаление сетевой карты с виртуальной машины
tooremove сетевой Адаптер из существующей виртуальной Машины, сначала освободить hello виртуальной Машины с [ВМ az deallocate](/cli/azure/vm#deallocate). Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Удалите hello сетевого Адаптера с [удалите сетевой адаптер виртуальной машины az](/cli/azure/vm/nic#remove). Hello следующий пример удаляет *myNic3* из *myVM*:

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

Запуск hello виртуальной Машины с [запуска виртуальной машины az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a>Создание нескольких сетевых карт с помощью шаблонов Resource Manager
Шаблоны Azure Resource Manager среду использовать декларативные toodefine файлы JSON. Дополнительные сведения см. в [обзоре Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Шаблоны диспетчера ресурсов предоставить несколько экземпляров ресурса toocreate образом во время развертывания, таких как создание нескольких сетевых адаптеров. Вы используете *копирования* toospecify hello число экземпляров toocreate:

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

Вы можете прочитать дополнительные сведения о [создании нескольких экземпляров с помощью объекта *copy*](../../resource-group-create-multiple.md). 

Можно также использовать `copyIndex()` toothen Добавление номеров tooa имя ресурса, позволяющий toocreate `myNic1`, `myNic2`, т. д. hello ниже показан пример добавления hello значение индекса:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Вы можете ознакомиться с полным примером [создания нескольких сетевых карт с помощью шаблонов Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите [размеры виртуальных Машин Linux](sizes.md) при попытке toocreating виртуальной Машины с несколькими сетевыми адаптерами. Обратите внимание toohello максимальное количество сетевых адаптеров, размер каждой виртуальной Машины. 
