---
title: "aaaDeploy виртуальных машин Linux в существующей сети с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Узнайте, как toodeploy виртуальной машины Linux в существующей виртуальной сети с помощью hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a>Как toodeploy виртуальной машины Linux в существующей виртуальной сети Azure с hello Azure CLI

В этой статье показано, как toouse hello Azure CLI 2.0 toodeploy виртуальной машины (VM) в рамках существующей виртуальной сети. Существуют следующие требования Hello.

- [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);
- [файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md).

Можно также выполнить следующие действия с hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).


## <a name="quick-commands"></a>Быстрые команды
Если вам требуется tooquickly выполнения задачи hello, hello в следующем разделе подробно описываются hello команд, которые необходимы. Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#detailed-walkthrough).

toocreate этой пользовательской среды hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.

**Предварительные требования:** группа ресурсов Azure, виртуальная сеть и подсеть, группа безопасности сети с разрешенными входящими подключениями SSH и виртуальная сетевая карта.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Развертывание hello виртуальных Машин в инфраструктуре виртуальной сети hello

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство

Ресурсы Azure, такие как виртуальные сети и группы безопасности сети, должны быть статическими. Они должны долго храниться и редко развертываться. После развертывания виртуальной сети, он может быть использован в новые развертывания без инфраструктуры toohello любой негативно влияет на. Подумайте о виртуальной сети как сетевой коммутатор традиционных оборудования - не потребовалось бы tooconfigure нового оборудования переключиться с каждым развертыванием. С правильно настроенной виртуальной сети, вы можете продолжить toodeploy новые виртуальные машины в виртуальной сети с минимальными снова и снова при его наличии, изменения требуются протяжении hello hello виртуальной сети.

toocreate этой пользовательской среды hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.

## <a name="create-hello-resource-group"></a>Создать группу ресурсов hello

Во-первых создайте tooorganize группы ресурсов Azure все данные, создаваемые в данном пошаговом руководстве. Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Создать группу ресурсов hello с [Создание группы az](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a>Создайте виртуальную сеть hello

Позволяет построения виртуальных машин в виртуальной сети Azure toolaunch hello. Дополнительные сведения о виртуальных сетях см. в разделе [Создание виртуальной сети с помощью Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md). Создайте виртуальную сеть hello с [создания az сети vnet](/cli/azure/network/vnet#create). Hello следующий пример создает виртуальную сеть с именем *myVnet* и подсеть с именем *mySubnet*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a>Создание группы безопасности сети hello

Эквивалентный tooa брандмауэра на уровне сети hello являются группы безопасности сети Azure. Дополнительные сведения о группах сетевой безопасности см. в разделе [Сопоставление групп безопасности сети toocreate в hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md). Создание группы безопасности сети hello с [создать az сети nsg](/cli/azure/network/nsg#create). Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Добавление правила, разрешающего входящий трафик по протоколу SSH

Hello виртуальной Машины требуется доступ из hello необходима Интернета, поэтому правило, разрешающее трафик toobe входящий порт 22 передаются через tooport сети hello 22 hello виртуальной Машины. Добавьте правило входящего трафика для hello сетевой группы безопасности с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create). Hello следующий код создает правило с именем *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a>Присоединение группы безопасности сети toohello подсети hello

правила группы сетевой безопасности Hello может быть применен tooa подсети или определенного виртуального сетевого интерфейса. Позволяет присоединить подсеть tooour группы безопасности сети hello. Присоединение к подсети toohello сетевой группы безопасности с [обновления подсети виртуальной сети сети az](/cli/azure/network/vnet/subnet#update):

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a>Добавить подсеть toohello карты виртуального сетевого интерфейса

Виртуальных сетевых картах (VNics) являются важной, так как можно повторно использовать их, подключив их toodifferent виртуальных машин. Повторное использование позволяет tookeep hello виртуального сетевого адаптера как статический ресурс, а hello виртуальные машины могут быть как временными. Создание виртуального сетевого адаптера и связать его с hello подсети с [Создание сетевого адаптера сети az](/cli/azure/network/nic#create). Hello следующем примере создается виртуальный сетевой адаптер с именем *myNic*:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Развертывание hello виртуальных Машин в инфраструктуре виртуальной сети hello

Теперь у вас есть виртуальная сеть и подсеть и подсеть hello tooprotect группы безопасности сети, блокируя весь входящий трафик, за исключением порт 22 для SSH. Теперь может быть развернут Hello виртуальной Машины внутри этой существующей сетевой инфраструктуре.

Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). Дополнительные сведения о hello флаги toouse с toodeploy hello Azure CLI 2.0 завершения виртуальной Машины, см. в разделе [создать полную среду Linux с помощью Azure CLI hello](create-cli-complete.md).

Следующий пример Hello создает виртуальную Машину с помощью управляемых дисков Azure. Эти диски обрабатываются hello платформы Azure и не требуют toostore любые предварительные и место их. Дополнительные сведения об управляемых дисках Azure см. в [этой статье](../../storage/storage-managed-disks-overview.md). При желании toouse неуправляемого дисков см. Примечание дополнительных hello ниже.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

Если вы используете управляемые диски, пропустите этот шаг. При желании toouse неуправляемого дисков требуется hello tooadd следующие дополнительные параметры toohello продолжением команда toocreate неуправляемого дисков в hello учетной записи хранилища с именем `mystorageaccount`: 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

С помощью hello CLI флаги toocall существующие ресурсы, вы указываете hello Azure toodeploy виртуальных Машин в существующей сети hello. После развертывания виртуальную сеть и подсеть можно оставить в качестве статических или постоянных ресурсов в регионе Azure. В этом примере не не создать и назначить открытый IP адрес toohello виртуального сетевого адаптера, поэтому эту виртуальную Машину не доступен из Интернета через Интернет hello. Дополнительные сведения см. в разделе [Создание ВМ с статический общедоступный IP-адрес с помощью Azure CLI hello](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о способах toocreate виртуальных машин в Azure см. в разделе hello следующие ресурсы:

* [Использовать toocreate шаблона диспетчера ресурсов Azure конкретного развертывания](../windows/cli-deploy-templates.md)
* [Создание полной среды Linux с помощью интерфейса командной строки Azure](create-cli-complete.md)
* [Создание виртуальной машины Linux с помощью шаблона Azure](create-ssh-secured-vm-from-template.md)
