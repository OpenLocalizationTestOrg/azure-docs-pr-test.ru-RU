---
title: "aaaDeploy виртуальных машин Linux в существующей сети с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Как toodeploy виртуальной Машины Linux в существующей виртуальной сети с помощью hello Azure CLI 1.0"
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
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a>Как toodeploy виртуальной машины Linux в существующей виртуальной сети Azure с hello Azure CLI 1.0

В этой статье показано, как toodeploy toouse Azure CLI 1.0 виртуальной машины (VM) в существующей виртуальной сети (VNet). Существуют следующие требования Hello.

- [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);
- [файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md).


## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления


## <a name="quick-commands"></a>Быстрые команды

Если вам требуется tooquickly выполнения задачи hello, hello в следующем разделе подробно описываются hello команд, которые необходимы. Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Необходимые компоненты: группа ресурсов, виртуальная сеть, группа безопасности сети с входящим трафиком SSH, подсеть. Замените все примеры параметров своими параметрами.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Развертывание hello виртуальных Машин в инфраструктуре виртуальной сети hello

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство

Активов Azure, такие как hello виртуальных сетей и группы безопасности сети должен быть статическим и долго ресурсы, которые развертываются редко. После развертывания виртуальной сети, он может быть использован в новые развертывания без инфраструктуры toohello любой негативно влияет на. Представьте виртуальную сеть, как сетевой коммутатор в парадигме традиционного оборудования. Вы не должны были tooconfigure нового оборудования переключиться с каждым развертыванием. С правильно настроенной виртуальной сети можно будет продолжить toodeploy новых серверов в этой виртуальной сети и снова несколько, если таковые имеются, изменения, необходимые протяжении hello hello виртуальной сети.

## <a name="create-hello-resource-group"></a>Создать группу ресурсов hello

Сначала необходимо создаете группы ресурсов tooorganize все данные, создаваемые в данном пошаговом руководстве. Дополнительные сведения о группах ресурсов см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a>Создать hello виртуальной сети

Hello первым шагом является toobuild виртуальных машин в hello toolaunch виртуальной сети. Hello виртуальная сеть содержит одну подсеть для этого пошагового руководства. Дополнительные сведения о виртуальных сетях Azure см. в разделе [Создание виртуальной сети с помощью hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a>Создание группы безопасности сети hello

подсети Hello построена за существующей сетевой группы безопасности таким образом построить hello сетевой группы безопасности перед hello подсети. Эквивалентный tooa брандмауэра на уровне сети hello являются группы безопасности сети Azure. Дополнительные сведения о группах безопасности сети Azure см. в разделе [Сопоставление групп безопасности сети toocreate в hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Добавление правила, разрешающего входящий трафик по протоколу SSH

Hello виртуальной Машины требуется доступ из hello необходима Интернета, правило, разрешающее трафик toobe входящий порт 22 передаются через tooport сети hello 22 hello виртуальной Машины.

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Добавить toohello подсети виртуальной сети

Виртуальные машины в виртуальной сети hello должна находиться в подсети. Каждая виртуальная сеть может содержать несколько подсетей. Создать подсеть hello и связать с группой безопасности сети hello.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Теперь Hello подсети добавляется внутри hello виртуальной сети и связанные с группой безопасности сети hello и правила.


## <a name="add-a-vnic-toohello-subnet"></a>Добавить подсеть toohello виртуального сетевого адаптера

Виртуальные сетевые адаптеры (VNics) являются важными, как можно повторно использовать их, подключив их toodifferent виртуальных машин. Этот подход позволяет hello виртуального сетевого адаптера как статический ресурс, пока hello виртуальные машины могут быть как временными. Создание виртуального сетевого адаптера и связать его с подсетью hello на предыдущем шаге hello.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Развертывание hello виртуальной Машины в виртуальной сети hello и NSG

Теперь у вас есть виртуальная сеть и подсети в этой виртуальной сети и группа безопасности сети выступает tooprotect hello подсети, блокируя весь входящий трафик, за исключением порт 22 для SSH. Теперь может быть развернут Hello виртуальной Машины внутри этой существующей сетевой инфраструктуре.

С помощью Azure CLI hello и hello `azure vm create` команды hello виртуальных Машин Linux — развернутой toohello существующие группы ресурсов Azure, виртуальной сети, подсети и виртуального сетевого адаптера. Дополнительные сведения об использовании toodeploy CLI hello завершения виртуальной Машины в разделе [создать полную среду Linux с помощью hello Azure CLI](create-cli-complete.md)

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

С помощью hello CLI флаги toocall существующие ресурсы, вы указываете hello Azure toodeploy виртуальных Машин в существующей сети hello. После развертывания виртуальную сеть и подсеть можно оставить в качестве статических или постоянных ресурсов в регионе Azure.  

## <a name="next-steps"></a>Дальнейшие действия

* [Использовать toocreate шаблона диспетчера ресурсов Azure конкретного развертывания](../windows/cli-deploy-templates.md)
* [Создание полной среды Linux с помощью интерфейса командной строки Azure](create-cli-complete.md)
* [Создание виртуальной машины Linux с помощью шаблона Azure](create-ssh-secured-vm-from-template.md)
