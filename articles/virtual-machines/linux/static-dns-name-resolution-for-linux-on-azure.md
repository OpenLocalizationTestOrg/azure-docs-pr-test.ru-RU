---
title: "aaaUse внутренние DNS для виртуальной Машины имен с hello Azure CLI 2.0 | Документы Microsoft"
description: "Как карт toocreate виртуальной сети и использовать внутренние DNS для разрешения имен виртуальных Машин в Azure с hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a>Создание виртуальных сетевых карт и использование внутренних DNS-имен для разрешения имен виртуальных машин в Azure
В этой статье показано, как tooset статические внутренние имена DNS для виртуальных машин Linux с помощью виртуальных сетевых интерфейсных плат (vNics) и DNS-имена меток с hello Azure CLI 2.0. Можно также выполнить следующие действия с hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Статические имена DNS используются для постоянных инфраструктурных служб, таких как сервер сборки Jenkins, который используется для этого поддержания документа, или сервер Git.

Существуют следующие требования Hello.

* [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);
* [файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Быстрые команды
Если вам требуется tooquickly выполнения задачи hello, hello в следующем разделе подробно описываются hello команд, которые необходимы. Более подробные сведения и контекста, для каждого шага можно найти в hello остальной части документа hello [начиная здесь](#detailed-walkthrough). tooperform эти шаги, необходимые hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

Предварительные требования: группа ресурсов, виртуальная сеть и подсеть, группа безопасности сети с разрешенными входящими подключениями SSH.

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a>Создание виртуальной сетевой карты со статическим внутренним DNS-именем
Создание виртуального сетевого адаптера hello с [Создание сетевого адаптера сети az](/cli/azure/network/nic#create). Hello `--internal-dns-name` CLI флаг предназначен для параметра hello DNS метку, которую предоставляет hello статических DNS-имя для hello виртуальный сетевой адаптер (vNic). Hello следующем примере создается виртуальный сетевой адаптер с именем `myNic`, подключает его toohello `myVnet` виртуальной сети и создает внутренние DNS-имя запись вызывается `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a>Развертывание виртуальной Машины и подключение виртуального сетевого адаптера hello
Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). Hello `--nics` флаг подключается toohello hello виртуального сетевого адаптера виртуальной Машины во время развертывания tooAzure hello. Hello следующий пример создает Виртуальную машину с именем `myVM` с дисками управляемых Azure и присоединяет виртуального сетевого адаптера hello с именем `myNic` из предыдущих шага hello:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство

Полная непрерывной интеграции и непрерывного развертывания (CiCd) инфраструктуру в Azure требует определенных серверов toobe статической или долгоживущие серверов. Рекомендуется являются статическими активов Azure как hello виртуальных сетей и группы безопасности сети, а также долго ресурсы, которые развертываются редко. После развертывания виртуальной сети, он может быть использован в новые развертывания без инфраструктуры toohello любой негативно влияет на. Позднее можно добавить сервер репозитория Git или сервер автоматизации Jenkins доставляет CiCd toothis виртуальной сети для сред разработки и тестирования.  

Внутренние имена DNS можно сопоставлять только внутри виртуальной сети Azure. Так как hello DNS-имена являются внутренними, они не удается разрешить toohello за пределами Интернет, обеспечивая дополнительную безопасность инфраструктуры toohello.

В hello следующих примерах замените примеры имен параметров собственные значения. Используемые имена параметров: `myResourceGroup`, `myNic` и `myVM`.

## <a name="create-hello-resource-group"></a>Создать группу ресурсов hello
Во-первых, создать группу ресурсов hello с [Создание группы az](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westus` расположение:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a>Создайте виртуальную сеть hello

Hello следующим шагом является toobuild виртуальных машин в hello toolaunch виртуальной сети. Hello виртуальная сеть содержит одну подсеть для этого пошагового руководства. Дополнительные сведения о виртуальных сетях Azure см. в разделе [Создание виртуальной сети с помощью Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Создайте виртуальную сеть hello с [создания az сети vnet](/cli/azure/network/vnet#create). Hello следующий пример создает виртуальную сеть с именем `myVnet` и подсеть с именем `mySubnet`:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a>Создание группы безопасности сети hello
Эквивалентный tooa брандмауэра на уровне сети hello являются Azure группы безопасности сети. Дополнительные сведения о сетевых группах безопасности см. в разделе [как Nsg toocreate в hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Создание группы безопасности сети hello с [создать az сети nsg](/cli/azure/network/nsg#create). Hello следующий пример создает группу безопасности сети с именем `myNetworkSecurityGroup`:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a>Добавить правило для входящего трафика tooallow SSH
Добавьте правило входящего трафика для hello сетевой группы безопасности с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create). Hello следующий код создает правило с именем `myRuleAllowSSH`:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a>Свяжите hello подсеть с hello группы безопасности сети
Используйте подсеть hello tooassociate с hello сетевой группы безопасности, [обновления подсети виртуальной сети сети az](/cli/azure/network/vnet/subnet#update). Hello следующий пример сопоставляет имя подсети hello `mySubnet` с hello сетевую группу безопасности с именем `myNetworkSecurityGroup`:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a>Создайте виртуальный сетевой адаптер hello и статические имена DNS
Azure обладает большой гибкостью, однако toouse DNS-имен для разрешения имен виртуальных Машин, требуют toocreate виртуальных сетевых картах (vNics), включающие метка DNS. vNics являются важными, как можно повторно использовать их, подключив их виртуальные машины toodifferent над жизненным циклом инфраструктуры hello. Этот подход позволяет hello виртуального сетевого адаптера как статический ресурс, пока hello виртуальные машины могут быть как временными. С помощью DNS, пометки hello виртуальный сетевой адаптер, не может tooenable простое имя разрешения из других виртуальных машин в виртуальной сети hello. С помощью разрешения имен включает другие виртуальные машины сервера автоматизации hello tooaccess hello DNS-именем `Jenkins` или сервера hello Git в качестве `gitrepo`.  

Создание виртуального сетевого адаптера hello с [Создание сетевого адаптера сети az](/cli/azure/network/nic#create). Hello следующем примере создается виртуальный сетевой адаптер с именем `myNic`, подключает его toohello `myVnet` виртуальная сеть с именем `myVnet`и создает внутренние DNS-имя запись вызывается `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Развертывание hello виртуальных Машин в инфраструктуре виртуальной сети hello
Теперь имеется виртуальной сети и подсети, группы безопасности сети, выступающего в качестве tooprotect брандмауэра нашей подсети, блокируя весь входящий трафик, за исключением порт 22 для SSH и виртуального сетевого адаптера. Теперь вы можете развернуть виртуальную машину в этой созданной сетевой инфраструктуре.

Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). Hello следующий пример создает Виртуальную машину с именем `myVM` с дисками управляемых Azure и присоединяет виртуального сетевого адаптера hello с именем `myNic` из предыдущих шага hello:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

С помощью hello CLI флаги toocall существующие ресурсы мы поручить Azure toodeploy hello виртуальных Машин в существующей сети hello. tooreiterate, после развертывания виртуальной сети и подсети они могут остаться статические или постоянным ресурсов в ваш регион Azure.  

## <a name="next-steps"></a>Дальнейшие действия
* [Создание полной среды Linux с помощью интерфейса командной строки Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Создание виртуальной машины Linux с помощью шаблона Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
