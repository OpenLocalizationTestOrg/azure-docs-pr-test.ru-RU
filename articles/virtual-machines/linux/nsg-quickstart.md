---
title: "aaaOpen порты tooa виртуальных Машин Linux с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Узнайте, как tooopen порт / create tooyour конечной точки виртуальной Машины с Linux с помощью развертывания диспетчера ресурсов Azure hello модели и hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a>Откройте порты и конечные точки tooa виртуальных Машин Linux с hello Azure CLI
Открытие порта, или создайте конечную точку, tooa виртуальной машины (VM в Azure, создав фильтр сети для подсети или сетевому интерфейсу виртуальной Машины). Эти фильтры, которые позволяют управлять входящего и исходящего трафика, поместите на ресурсе toohello вложенные группы безопасности сети, который принимает трафик hello. Давайте используем распространенный пример веб-трафика через порт 80. В этой статье показано, как tooopen tooa порт виртуальной Машины с hello Azure CLI 2.0. Можно также выполнить следующие действия с hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).


## <a name="quick-commands"></a>Быстрые команды
Группы безопасности сети toocreate и правила, которые требуется последняя версия hello [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.

Создание группы безопасности сети hello с [создать az сети nsg](/cli/azure/network/nsg#create). Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup* в hello *eastus* расположение:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Добавить правило с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) tooallow HTTP-трафик, tooyour веб-сервер (или настроить для собственных сценариев, например для подключения SSH access или базы данных). Hello следующий код создает правило с именем *myNetworkSecurityGroupRule* tooallow TCP-трафик через порт 80:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

Связать hello сетевой группы безопасности с сетевым интерфейсом Виртуальной машины (NIC) с [обновления сетевого адаптера сети az](/cli/azure/network/nic#update). Hello следующий пример сопоставляет существующего сетевого Адаптера с именем *myNic* с hello сетевую группу безопасности с именем *myNetworkSecurityGroup*:

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

Кроме того, можно поставить в вашей группе безопасности сети подсети виртуальной сети с [обновления подсети виртуальной сети сети az](/cli/azure/network/vnet/subnet#update) вместо просто toohello сетевого интерфейса на одной виртуальной Машины. Hello следующем примере производится связывание существующей подсети с именем *mySubnet* в hello *myVnet* виртуальную сеть с hello сетевую группу безопасности с именем *myNetworkSecurityGroup*:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a>Дополнительная информация о группах безопасности сети
Hello здесь Быстрые команды позволяют tooget вверх и работает с tooyour передачу трафика виртуальных Машин. Сетевые группы безопасности предоставляют много замечательных функций и гранулярности для управления доступа к ресурсам tooyour. [Здесь](tutorial-virtual-network.md#secure-network-traffic)вы можете больше прочитать о создании группы безопасности сети и правил ACL.

Для веб-приложений с высокой доступностью необходимо поместить виртуальную машину за Azure Load Balancer. Подсистема балансировки нагрузки Hello распределяет трафик tooVMs, с группой безопасности сети, которая обеспечивает фильтрацию трафика. Дополнительные сведения см. в разделе [как баланс tooload Linux виртуальных машин в Azure toocreate приложение с высокой доступностью](tutorial-load-balancer.md).

## <a name="next-steps"></a>Дальнейшие действия
В этом примере вы создали трафика tooallow HTTP простое правило. Можно найти сведения о создании более подробные сред в hello в следующих статьях:

* [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md)
