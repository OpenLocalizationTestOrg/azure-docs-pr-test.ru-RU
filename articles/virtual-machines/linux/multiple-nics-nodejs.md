---
title: "aaaCreate виртуальной Машины Linux в Azure с несколькими сетевыми адаптерами | Документы Microsoft"
description: "Узнайте, как toocreate ВМ Linux с несколькими сетевыми адаптерами присоединенного tooit с помощью шаблонов hello Azure CLI или диспетчер ресурсов."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a>Создание виртуальной машины Linux с несколькими сетевыми адаптерами, используя hello Azure CLI 1.0
Можно создать виртуальную машину (ВМ) в Azure, которая имеет несколько tooit интерфейсов (NIC), подключенных виртуальных сетей. Типичный сценарий состоит в разных подсетях toohave для внешнего и внутреннего интерфейса подключения или сеть, выделенная tooa наблюдения или решение для резервного копирования. Эта статья содержит toocreate Быстрые команды виртуальной Машины с несколькими tooit присоединенного сетевых адаптеров. Подробные сведения, включая как toocreate несколько сетевых адаптеров в собственных Bash скрипты, Дополнительные сведения о [развертывание виртуальных машин multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Различные [размеры виртуальных машин](sizes.md) поддерживают разное число сетевых карт, так что выбирайте соответствующий размер виртуальной машины.

> [!WARNING]
> Необходимо подключить несколько сетевых адаптеров, после создания виртуальной Машины — не удается добавить существующие ВМ в Azure CLI 1.0 hello tooan сетевых адаптеров. Вы можете [добавить существующие ВМ в Azure CLI 2.0 hello tooan сетевые адаптеры](multiple-nics.md). Вы также можете [создания основании hello исходные виртуальные диски виртуальной Машины](copy-vm.md) и создать несколько сетевых адаптеров, при развертывании виртуальной Машины hello.


## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#create-supporting-resources) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](multiple-nics.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления


## <a name="create-supporting-resources"></a>Создание вспомогательных ресурсов
Убедитесь, что имеется hello [Azure CLI](../../cli-install-nodejs.md) входа в систему и использование режима диспетчера ресурсов:

```azurecli
azure config mode arm
```

В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.

Сначала создайте группу ресурсов. Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:

```azurecli
azure group create myResourceGroup --location eastus
```

Создание учетной записи хранилища toohold виртуальных машин. Hello следующий пример создает учетную запись хранения с именем *mystorageaccount*:

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

Создайте виртуальные машины tooconnect виртуальной сети. Hello следующий пример создает виртуальную сеть с именем *myVnet* с префикс адреса *192.168.0.0/16*:

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

Создайте две подсети виртуальной сети — для интерфейсного трафика и для внутреннего трафика. Hello следующий пример создает две подсети, с именем *mySubnetFrontEnd* и *mySubnetBackEnd*:

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a>Создание и настройка нескольких сетевых карт
Можно прочитать дополнительные сведения о [развертывание нескольких сетевых адаптеров с помощью Azure CLI hello](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), включая сценарии процесс hello циклический перебор toocreate всех сетевых адаптеров hello.

Hello следующий пример создает два сетевых адаптера с именем *myNic1* и *myNic2*, с одним сетевым Адаптером подключение tooeach подсети:

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

Обычно также создать [сетевой группы безопасности](../../virtual-network/virtual-networks-nsg.md) или [подсистемы балансировки нагрузки](../../load-balancer/load-balancer-overview.md) toohelp управлять и распределять трафик между виртуальных машин. Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup*:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Привязать вашей группы безопасности сети toohello сетевых адаптеров с помощью `azure network nic set`. Hello следующего примера производится привязка *myNic1* и *myNic2* с *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Создайте виртуальную Машину и присоединения hello сетевых адаптеров
При создании виртуальной Машины hello, теперь указать несколько сетевых адаптеров. Вместо этого с помощью `--nic-name` tooprovide один сетевой Адаптер, вместо этого используйте `--nic-names` и указать список разделенных запятыми сетевых адаптеров. Необходимо также tootake осторожность при выборе hello размер виртуальной Машины. Существуют ограничения для hello общее число сетевых адаптеров, вы можете добавить tooa виртуальной Машины. Прочитайте дополнительные сведения о [размерах виртуальных машин Linux](sizes.md). Hello следующем примере показано, как toospecify несколько сетевых адаптеров, а затем виртуальной Машины размера, поддерживает использование нескольких сетевых адаптеров (*Standard_DS2_v2*):

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
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
Убедитесь, что tooreview [размеры виртуальных Машин Linux](sizes.md) при попытке toocreating виртуальной Машины с несколькими сетевыми адаптерами. Обратите внимание toohello максимальное количество сетевых адаптеров, размер каждой виртуальной Машины. 

Помните, что нельзя добавить дополнительные tooan сетевые адаптеры с существующей виртуальной Машины, при развертывании hello виртуальной Машины необходимо создать все сетевые адаптеры hello. Будьте внимательны при планировании вашего развертывания toomake наличие всех необходимых hello сетевые соединения с самого начала hello.

