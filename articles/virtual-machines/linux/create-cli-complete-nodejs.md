---
title: "aaaCreate полную среду Linux с hello Azure CLI 1.0 | Документы Microsoft"
description: "Создайте хранилища, виртуальной Машины Linux, виртуальной сети и подсети, подсистемы балансировки нагрузки, сетевой Адаптер, общедоступный IP-адрес и группу безопасности сети из hello основание, с помощью hello Azure CLI 1.0."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a>Создайте полную среду Linux с hello Azure CLI 1.0
В этой статье мы создаем простую сеть с балансировщиком нагрузки и парой виртуальных машин, подходящих для разработки и простых вычислений. Мы будем рассматривать процесса hello, команда, пока не получится два рабочий защитить toowhich виртуальных машин Linux, которым можно подключаться из в любом месте на hello Интернет. Затем можно переместить на toomore сложная топология сетей и сред.

Вдоль hello образом вы узнаете о hello зависимостей иерархии дает hello модели развертывания диспетчера ресурсов, что о сведения о количестве энергии предоставляет. После появления построение hello системы можно перестроить его гораздо быстрее с помощью [шаблоны Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Кроме того после вы узнаете, как взаимодействуют hello части среды, создание шаблонов tooautomate их становится проще.

Среда Hello содержит:

* две виртуальные машины в группе доступности;
* балансировщик нагрузки с правилом балансировки нагрузки для порта 80;
* Группы безопасности сети (NSG) правила tooprotect ВМ от нежелательного трафика.

toocreate этой пользовательской среды необходимо hello последней [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) в режим диспетчера ресурсов (`azure config mode arm`). Кроме того, потребуется инструмент анализа JSON. В этом примере используются [jq](https://stedolan.github.io/jq/).


## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления


## <a name="quick-commands"></a>Быстрые команды
При необходимости tooquickly выполнения задачи hello, hello следующий раздел сведения hello базовые команды tooupload tooAzure виртуальной Машины. Более подробные сведения и контекста, для каждого шага можно найти в hello остальной части документа hello, начиная [здесь](#detailed-walkthrough).

Убедитесь, что [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) входа в систему и использование режима диспетчера ресурсов:

```azurecli
azure config mode arm
```

В hello следующих примерах замените примеры имен параметров собственные значения. Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.

Создайте группу ресурсов hello. Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westeurope` расположение:

```azurecli
azure group create -n myResourceGroup -l westeurope
```

Проверьте hello группы ресурсов с помощью средства синтаксического анализа JSON hello:

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Создайте учетную запись хранения hello. Hello следующий пример создает учетную запись хранения с именем `mystorageaccount`. (имя учетной записи хранения hello должно быть уникальным, поэтому ввести уникальное имя).

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

Проверьте hello учетной записи хранилища с помощью средства синтаксического анализа JSON hello:

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

Создайте виртуальную сеть hello. Hello следующий пример создает виртуальную сеть с именем `myVnet`:

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

Создайте подсеть. Hello следующий пример создает подсеть с именем `mySubnet`:

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

Проверьте hello виртуальной сети и подсети с помощью средства синтаксического анализа JSON hello:

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Создайте общедоступный IP-адрес. Hello следующий пример создает общедоступный IP-адрес с именем `myPublicIP` с именем DNS hello `mypublicdns`. (hello DNS-имя должно быть уникальным, поэтому ввести уникальное имя).

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

Создайте hello подсистемы балансировки нагрузки. Hello следующий пример создает подсистемы балансировки нагрузки с именем `myLoadBalancer`:

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

Создать пул IP переднего плана для подсистемы балансировки нагрузки hello и свяжите hello общедоступный IP-адрес. Hello следующий пример создает интерфейсный IP пул с именем `mySubnetPool`:

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

Создайте пул IP-hello внутренней подсистемы балансировки нагрузки hello. Hello следующем примере создается пул IP серверной части, с именем `myBackEndPool`:

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

Создание правила преобразования адресов (NAT) для балансировки нагрузки hello входящего сетевого SSH. Hello следующий пример создает два правила подсистемы балансировки нагрузки, `myLoadBalancerRuleSSH1` и `myLoadBalancerRuleSSH2`:

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

Создание веб-hello входящих правил NAT для hello подсистемы балансировки нагрузки. Hello следующий пример создает правила подсистемы балансировки нагрузки с именем `myLoadBalancerRuleWeb`:

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

Создайте зонда работоспособности подсистемы балансировки нагрузки hello. Hello следующий пример создает TCP Проба с именем `myHealthProbe`:

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

Проверьте hello балансировки нагрузки, пулы IP-адресов и правила NAT с помощью средства синтаксического анализа JSON hello:

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

Создайте hello первый сетевой адаптер (NIC). Замените hello `#####-###-###` секции с идентификатором подписки Azure Идентификатор, указывается в выходные данные hello подписки **jq** при исследовании hello ресурсов, вы создаете. Кроме того, его можно просмотреть, выполнив команду `azure account list`.

Hello следующий пример создает сетевой Адаптер с именем `myNic1`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

Создание hello второй сетевой адаптер. Hello следующий пример создает сетевой Адаптер с именем `myNic2`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

Проверьте hello двух сетевых адаптеров с помощью средства синтаксического анализа JSON hello:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

Создание группы безопасности сети hello. Hello следующий пример создает группу безопасности сети с именем `myNetworkSecurityGroup`:

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

Добавьте два правила для входящих подключений для hello сетевой группы безопасности. Hello в примере создаются два правила, `myNetworkSecurityGroupRuleSSH` и `myNetworkSecurityGroupRuleHTTP`:

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

Проверьте группы безопасности сети hello и правила для входящих подключений с помощью средства синтаксического анализа JSON hello:

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

Привязать hello сетевой безопасности группы toohello двух сетевых адаптеров:

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

Создайте набор доступности hello. Hello следующий пример создает именованный набор доступности `myAvailabilitySet`:

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

Создание hello первая виртуальная машина Linux. Hello следующий пример создает Виртуальную машину с именем `myVM1`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Создать hello второй виртуальной Машины с Linux. Hello следующий пример создает Виртуальную машину с именем `myVM2`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Используйте tooverify средство синтаксического анализа JSON hello, что было создано все:

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

Экспорт вашей новой среды tooa шаблона tooquickly повторного создания новых экземпляров.

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство
Hello подробные инструкции, следующие за объяснить действия каждой команды при построении масштабирование среды. Эти понятия помогут вам при создании пользовательских сред для разработки или эксплуатации.

Убедитесь, что [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) входа в систему и использование режима диспетчера ресурсов:

```azurecli
azure config mode arm
```

В hello следующих примерах замените примеры имен параметров собственные значения. Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.

## <a name="create-resource-groups-and-choose-deployment-locations"></a>Создание групп ресурсов и выбор расположений развертывания
Группы ресурсов Azure — Логическое развертывание сущности, которые содержат конфигурации сведения метаданных tooenable hello логического управления и развертывания ресурсов. Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westeurope` расположение:

```azurecli
azure group create --name myResourceGroup --location westeurope
```

Выходные данные:

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a>Создайте учетную запись хранения.
Необходимые учетные записи хранения для дисков виртуальной Машины, а также для любых дополнительных дисков данных, которые должны tooadd. Учетные записи хранения создаются практически сразу после создания групп ресурсов.

Здесь мы используем hello `azure storage account create` команды, передав hello расположение учетной записи hello, hello группы ресурсов, которая управляет и hello тип поддержки хранения данных необходимо. Hello следующий пример создает учетную запись хранения с именем `mystorageaccount`:

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

Выходные данные:

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

ресурс группы с помощью hello tooexamine `azure group show` команды, воспользуемся hello [jq](https://stedolan.github.io/jq/) инструментов вместе с hello `--json` параметр Azure CLI. (Можно использовать **jsawk** или любую библиотеку языка вы предпочитаете tooparse hello JSON.)

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Выходные данные:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

tooinvestigate hello учетной записи хранилища с помощью hello CLI, необходимо сначала имена учетных записей tooset hello и ключи. Замените имя hello hello учетной записи хранения в следующий пример с именем выбранного hello:

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

Это позволит с легкостью просматривать сведения о хранилище.

```azurecli
azure storage container list
```

Выходные данные:

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a>Создание виртуальной сети и подсети
Теперь ты tooneed toocreate виртуальная сеть в Azure и подсеть, в котором можно создавать виртуальные машины. Hello следующий пример создает виртуальную сеть с именем `myVnet` с hello `192.168.0.0/16` префикс адреса:

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

Выходные данные:

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

Опять же, давайте используйте параметр--json hello `azure group show` и `jq` toosee как мы создаем ресурсов. Теперь у нас есть ресурс `storageAccounts` и ресурс `virtualNetworks`.  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Выходные данные:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

Теперь давайте создадим подсети в hello `myVnet` виртуальной сети, в которой hello развернутых виртуальных машин. Мы используем hello `azure network vnet subnet create` команду вместе с ресурсами hello, мы уже создали: hello `myResourceGroup` группы ресурсов и hello `myVnet` виртуальной сети. В следующем примере hello, мы добавляем hello подсеть с именем `mySubnet` с префикс подсети адреса hello `192.168.1.0/24`:

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

Выходные данные:

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

Так как подсеть hello логически находится внутри виртуальной сети hello, мы просмотрите сведения о подсети hello с немного другой командой. Команда Hello, мы используем `azure network vnet show`, но мы продолжим выходных данных JSON hello tooexamine с помощью `jq`.

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Выходные данные:

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a>Создание общедоступного IP-адреса
Теперь давайте создадим hello общедоступный IP-адрес (PIP), будут назначены tooyour подсистемы балансировки нагрузки. Благодаря этому можно tooyour tooconnect виртуальных машин из hello Интернета с помощью hello `azure network public-ip create` команды. Так как адрес по умолчанию hello является динамическим, мы создадим именованную запись DNS в hello **cloudapp.azure.com** домена с помощью hello `--domain-name-label` параметр. Hello следующий пример создает общедоступный IP-адрес с именем `myPublicIP` с именем DNS hello `mypublicdns`. Поскольку hello DNS-имя должно быть уникальным, вы предоставляете собственное уникальное имя DNS:

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

Выходные данные:

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

Hello общедоступный IP-адрес является также верхнего уровня, чтобы можно было видеть его с `azure group show`.

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Выходные данные:

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

Можно выяснить, Дополнительные сведения о ресурсов, включая hello полное доменное имя (FQDN) подобласти hello с помощью hello полный `azure network public-ip show` команды. логически выделил Hello открытого ресурса IP-адреса, но определенный адрес еще не были назначены. tooobtain IP-адрес, ты tooneed балансировки нагрузки, который мы еще не создана.

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

Выходные данные:

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a>Создание балансировщика нагрузки и пулов IP-адресов
При создании подсистемы балансировки нагрузки можно toodistribute трафика между несколькими виртуальными машинами. Он также обеспечивает избыточность tooyour приложения, выполнив несколько виртуальных машин, которые отвечают toouser запросы в событии hello обслуживания или в больших нагрузках. Hello следующий пример создает подсистемы балансировки нагрузки с именем `myLoadBalancer`:

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

Выходные данные:

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

Наш балансировщик нагрузки выглядит пустым, поэтому давайте создадим несколько пулов IP-адресов. Мы хотим пулы toocreate двух IP-адресов для наших балансировки нагрузки, для внешнего интерфейса hello и для серверной части hello. внешний пул IP-адресов Hello публично видимыми. Это также toowhich расположение hello, которые будут назначены hello PIP, которая была создана ранее. Далее мы используем hello внутреннем пуле как расположение для наших tooconnect виртуальных машин для. Таким образом, hello трафик может проходить через toohello подсистемы балансировки нагрузки hello виртуальных машин.

Сначала создадим интерфейсный пул IP-адресов. Hello следующий пример создает внешний пул с именем `myFrontEndPool`:

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

Выходные данные:

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

Обратите внимание на то, как мы использовали hello `--public-ip-name` коммутатор toopass в hello `myPublicIP` , созданную ранее. Назначение hello открытый IP-адрес подсистемы балансировки нагрузки toohello позволяет tooreach виртуальные машины по Интернету hello.

Теперь создадим второй пул IP-адресов, на этот раз для внутреннего трафика. Hello следующий пример создает пул серверной части, с именем `myBackEndPool`:

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

Выходные данные:

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

Можно увидеть, насколько нашей подсистемы балансировки нагрузки путем поиска с `azure network lb show` и изучения выходных данных JSON hello:

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

Выходные данные:

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a>Создание правил NAT балансировщика нагрузки
tooget трафик через наших балансировки нагрузки, нам нужно toocreate правила преобразования сетевых адресов (NAT), указать входящих или исходящих действия. Можно указать протокол toouse hello, а затем сопоставление портов toointernal внешними портами в случае необходимости. В нашей среде давайте создадим некоторые правила, которые разрешают SSH через наших tooour подсистемы балансировки нагрузки виртуальных машин. Мы устанавливаем tooTCP toodirect порты 4222 и 4223 TCP-порт 22 на нашем виртуальных машин (которые мы создаем более поздней версии). Hello следующий код создает правило с именем `myLoadBalancerRuleSSH1` toomap TCP-порт 4222 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

Выходные данные:

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

Повторите процедуру hello второго правила NAT для SSH. Hello следующий код создает правило с именем `myLoadBalancerRuleSSH2` toomap TCP-порт 4223 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

Давайте также пойти дальше и создать правило NAT для TCP-порт 80 для веб-трафика, подключая пулы IP-адресов tooour правило hello. Если мы подключить tooan правило hello пула IP-вместо привязки tooour правило hello виртуальных машин по отдельности, мы можно добавить или удалить виртуальных машин из пула IP-hello. Подсистема балансировки нагрузки Hello автоматически корректируется hello поток трафика. Hello следующий код создает правило с именем `myLoadBalancerRuleWeb` toomap TCP-порт 80 tooport 80:

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

Выходные данные:

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a>Создание пробы работоспособности балансировщика нагрузки
Состояния проверки периодически проверок hello виртуальных машин, находящихся за нашей toomake подсистемы балансировки нагрузки, убедиться, что они операционной и отвечать на запросы toorequests, как определено. Если нет, они были удалены из tooensure операции, для которого пользователи не перенаправлен toothem. Можно определить пользовательские проверки для проверки работоспособности hello, вместе с интервалами и значения времени ожидания. Дополнительные сведения о пробах работоспособности см. в статье [Проверки балансировщика нагрузки](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Hello следующий пример создает TCP работоспособности проверяется именованный `myHealthProbe`:

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

Выходные данные:

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

Здесь мы указали интервал в 15 секунд для проверок работоспособности. Мы может пропустить более четырех зондов (одна минута) подсистемы балансировки нагрузки hello считает, что перестал работать, на которых размещены hello.

## <a name="verify-hello-load-balancer"></a>Проверьте hello балансировки нагрузки
Теперь делается hello конфигурации подсистемы балансировки нагрузки. Ниже приведены hello действия, предпринятые.

1. Вы создали балансировщик нагрузки.
2. Созданы переднего плана пула IP и назначена открытый tooit IP.
3. Потом вы создали внутренний пул IP-адресов, к которому могут подключаться виртуальные машины.
4. Вы создали правила NAT, которые разрешают ВМ toohello SSH для управления, а также правила, которое разрешает TCP-порт 80 для наших веб-приложения.
5. Вы добавили работоспособности проверки tooperiodically проверки hello виртуальных машин. Эта проверка работоспособности гарантирует, что пользователи не предпринять tooaccess виртуальной Машины, которая больше не работает или передача содержимого.

Давайте посмотрим, как теперь выглядит балансировщик нагрузки.

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

Выходные данные:

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a>Создать toouse сетевого Адаптера с hello ВМ Linux
Сетевые адаптеры программно недоступны, так как можно применять правила использования tootheir. Кроме того, можно использовать несколько сетевых карт. В следующих hello `azure network nic create` команды подключить пула IP-адресов Сетевых toohello нагрузки внутренней hello и связать его с hello трафика SSH toopermit правило NAT.

Замените hello `#####-###-###` секции с идентификатором подписки Azure Идентификатор, указывается в выходные данные hello подписки `jq` при исследовании hello ресурсов, вы создаете. Кроме того, его можно просмотреть, выполнив команду `azure account list`.

Hello следующий пример создает сетевой Адаптер с именем `myNic1`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

Выходные данные:

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

Hello сведений можно определить, проверив hello ресурсов напрямую. Просмотрите hello ресурсов с помощью hello `azure network nic show` команды:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

Выходные данные:

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

Теперь мы создадим hello второй сетевой Адаптер, подключение в пул IP-адресов серверной части tooour еще раз. Это правило время hello второй NAT разрешает трафик по протоколу SSH. Hello следующий пример создает сетевой Адаптер с именем `myNic2`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a>Создание группы безопасности сети и правил
Теперь мы создайте группу безопасности сети и hello входящие правила, контролирующие доступ toohello сетевого адаптера. Группа безопасности сети может быть применен tooa сетевой Адаптер или подсети. Определение правила toocontrol hello поток трафика и из него виртуальных машин. Hello следующий пример создает группу безопасности сети с именем `myNetworkSecurityGroup`:

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

Давайте добавим hello входящее правило для hello NSG tooallow входящих подключений через порт 22 (toosupport SSH). Hello следующий код создает правило с именем `myNetworkSecurityGroupRuleSSH` tooallow TCP через порт 22:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

Теперь добавим hello входящее правило для hello NSG tooallow входящих подключений через порт 80 (toosupport веб-трафик). Hello следующий код создает правило с именем `myNetworkSecurityGroupRuleHTTP` tooallow TCP через порт 80:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> Правило входящего трафика Hello является фильтром для входящих подключений. В этом примере выполняется привязка toohello NSG hello виртуальных машин виртуальный сетевой Адаптер, это означает, что любой запрос tooport 22 передается через toohello сетевого Адаптера на нашем виртуальной Машины. Это правило для входящего сетевого подключения, а не конечной точки, как это было бы в классическом развертывании. tooopen порт, необходимо оставить hello `--source-port-range` значение слишком "\*" tooaccept (значение по умолчанию hello) входящие запросы от **любой** запрашивает порта. Обычно порты являются динамическими.
>
>

## <a name="bind-toohello-nic"></a>Привязать toohello сетевого Адаптера
Привязать hello NSG toohello сетевых адаптеров. Мы должны tooconnect нашей сетевые адаптеры с нашей группой безопасности сети. Выполните обе команды toohook копирование оба наших сетевых адаптеров:

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a>"Создать группу доступности"
Группы доступности помогают распределить виртуальные машины между доменами сбоя и доменами обновления. Создадим группу доступности для виртуальных машин. Hello следующий пример создает именованный набор доступности `myAvailabilitySet`:

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

Домены сбоя определяют группу виртуальных машин, совместно использующих общий источник питания и сетевой коммутатор. По умолчанию hello виртуальных машин, настроенных в наборе доступности должны быть разделены между toothree домены сбоя. Hello идея заключается в том, что проблема оборудования в одном из этих доменов сбоя не влияет на каждой виртуальной Машины, на котором выполняется приложение. Azure автоматически распределяет виртуальные машины в доменах сбоя hello при помещении их в группу доступности.

Домены обновления указания групп виртуальных машин и физического оборудования, можно перезагрузить в hello то же время. порядок Hello перезагрузке доменов обновления могут быть непоследовательными во время планового обслуживания, но только одно обновление перезагружается одновременно. Опять же, Azure автоматически распределяет виртуальные машины между доменами обновления при помещении их в группу доступности.

Дополнительные сведения о [управление hello доступности виртуальных машин](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="create-hello-linux-vms"></a>Создание виртуальных машин Linux hello
Вы создали hello ресурсы хранилища и сети виртуальных машин toosupport, доступном через Интернет. Теперь давайте создадим эти виртуальные машины и защитим их ключом SSH без пароля. В этом случае мы будем toocreate Виртуальной машине Ubuntu на основании hello последних Результатов. Информацию об этом образе мы находим с помощью команды `azure vm image list`, как описано в статье о [поиске образов виртуальных машин Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Мы выбрали образ с помощью команды hello `azure vm image list westeurope canonical | grep LTS`. В этом случае мы используем `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`. Для последнего поля hello, мы передаем `latest` , чтобы в будущем hello мы всегда получать последнюю сборку hello. (мы используем строка hello `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).

Это следующий шаг — знакомый tooanyone, кто уже создал ssh открытого и закрытого ключей rsa сопряжения на Mac или Linux с помощью **ssh-keygen - t rsa -b 2048**. Если в вашем каталоге `~/.ssh` нет пар ключей сертификата, то их можно создать:

* Автоматически, с помощью hello `azure vm create --generate-ssh-keys` параметр.
* Вручную с помощью [toocreate инструкции hello их самостоятельно](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Кроме того, можно использовать hello `--admin-password` метод tooauthenticate создания подключений SSH после hello виртуальной Машины. Обычно этот метод менее безопасен.

Мы создаем hello виртуальной Машине путем подключения к нашей ресурсы и сведения, а также hello `azure vm create` команды:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Выходные данные:

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

Немедленно tooyour ВМ можно подключиться с помощью ключей SSH по умолчанию. Убедитесь, что указан соответствующий порт hello, так как мы передается через hello балансировки нагрузки. (Для нашей первая виртуальная машина подготовим hello NAT правило tooforward порт 4222 tooour виртуальной Машины.)

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

Выходные данные:

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

Создайте второй ВМ в hello так же:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Теперь можно использовать hello `azure vm show myResourceGroup myVM1` команды tooexamine вы создали. На данном этапе имеются работающие виртуальные машины Ubuntu, расположенные за балансировщиком нагрузки в Azure, входить на которые можно только с помощью пары ключей SSH (так как пароли отключены). Установить nginx или httpd, развертывание веб-приложения и видеть hello трафик проходил через hello tooboth подсистемы балансировки нагрузки виртуальных машин hello.

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

Выходные данные:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a>Экспорт hello среду как шаблон
Теперь после создания этой среды, что делать, если вы хотите toocreate среде дополнительная разработка с hello такими же параметрами или рабочей среде, которая сопоставляет его? Диспетчер ресурсов использует JSON шаблонов, определяющих все параметры hello для вашей среды. Можно полностью создавать среды, ссылаясь на этот шаблон JSON. Вы можете [вручную построить шаблоны JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или экспортировать существующий шаблон JSON hello toocreate среды:

```azurecli
azure group export --name myResourceGroup
```

Эта команда создает hello `myResourceGroup.json` файла в текущий рабочий каталог. При создании среды на основе этого шаблона, запрашиваются все имена ресурсов hello, включая имена hello для балансировки нагрузки hello, сетевые интерфейсы или виртуальных машин. Эти имена можно заполнить в файле шаблона, добавляя hello `-p` или `--includeParameterDefaultValue` toohello параметр `azure group export` команду, которая было показано ранее. Редактирование JSON шаблона toospecify hello имена ресурсов, или [создайте файл parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , указывающий имена ресурсов hello.

toocreate среды из шаблона:

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

Может потребоваться tooread [Дополнительные сведения о том, как toodeploy из шаблонов](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Сведения о средах обновление tooincrementally, использовать файл параметров hello и получить доступ к шаблонам с единым хранилища.

## <a name="next-steps"></a>Дальнейшие действия
Теперь вы готовы toobegin работа с несколькими сетевыми компонентами и виртуальные машины. Toobuild среды этот образец можно использовать из приложения с помощью hello основные компоненты представленные здесь.
