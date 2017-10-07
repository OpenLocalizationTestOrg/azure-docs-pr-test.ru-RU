---
title: "aaaOpen порты tooa виртуальных Машин Linux с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tooopen порт / create tooyour конечной точки виртуальной Машины с Linux с помощью развертывания диспетчера ресурсов Azure hello модели и hello Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a>Открытие портов и конечные точки tooa виртуальных Машин Linux в Azure с помощью hello Azure CLI 1.0
Открытие порта, или создайте конечную точку, tooa виртуальной машины (VM в Azure, создав фильтр сети для подсети или сетевому интерфейсу виртуальной Машины). Эти фильтры, которые позволяют управлять входящего и исходящего трафика, поместите на ресурсе toohello вложенные группы безопасности сети, который принимает трафик hello. Давайте используем распространенный пример веб-трафика через порт 80. В этой статье показано, как использование виртуальной Машины порт tooa tooopen hello Azure CLI 1.0.


## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](nsg-quickstart.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления


## <a name="quick-commands"></a>Быстрые команды
toocreate сетевой группы безопасности и правила необходимо [hello Azure CLI 1.0](../../cli-install-nodejs.md) установлен и использование режима диспетчера ресурсов:

```azurecli
azure config mode arm
```

В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.

Создайте группу безопасности сети, указав собственные имена и расположение. Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup* в hello *eastus* расположение:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Добавить веб-серверу трафика tooyour правило tooallow HTTP (или настроить для собственных сценариев, например для подключения SSH access или базы данных). Hello следующий код создает правило с именем *myNetworkSecurityGroupRule* tooallow TCP-трафик через порт 80:

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

Свяжите hello группы безопасности сети с Виртуальной машины сетевого интерфейса (NIC). Hello следующий пример сопоставляет существующего сетевого Адаптера с именем *myNic* с hello сетевую группу безопасности с именем *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

Кроме того можно связать вашей группе безопасности сети с подсеть виртуальной сети, а не просто toohello сетевого интерфейса на одной виртуальной Машины. Hello следующем примере производится связывание существующей подсети с именем *mySubnet* в hello *myVnet* виртуальную сеть с hello сетевую группу безопасности с именем *myNetworkSecurityGroup*:

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a>Дополнительная информация о группах безопасности сети
Hello здесь Быстрые команды позволяют tooget вверх и работает с tooyour передачу трафика виртуальных Машин. Сетевые группы безопасности предоставляют много замечательных функций и гранулярности для управления доступа к ресурсам tooyour. [Здесь](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)вы можете больше прочитать о создании группы безопасности сети и правил ACL.

Группы безопасности сети и правила ACL можно также определять в шаблонах Azure Resource Manager. Узнайте больше о [создании групп безопасности сети с помощью шаблонов](../../virtual-network/virtual-networks-create-nsg-arm-template.md).

Перенаправление портов toouse toomap внутренний порт tooan уникальный внешний порт на виртуальной Машине, используйте подсистему балансировки нагрузки и правила преобразования сетевых адресов (NAT). Например можно tooexpose TCP-порт 8080 извне и трафик, направленный tooTCP порт 80 на виртуальной Машине. Вы можете узнать о [создании балансировщика нагрузки с выходом в Интернет](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).

## <a name="next-steps"></a>Дальнейшие действия
В этом примере вы создали трафика tooallow HTTP простое правило. Можно найти сведения о создании более подробные сред в hello в следующих статьях:

* [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md)
* [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](../../load-balancer/load-balancer-arm.md)

