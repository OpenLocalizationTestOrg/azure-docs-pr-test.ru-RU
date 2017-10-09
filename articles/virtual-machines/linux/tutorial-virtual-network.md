---
title: "aaaAzure виртуальных сетей и виртуальных машин Linux | Документы Microsoft"
description: "Учебник - управление виртуальными сетями Azure и виртуальных машин Linux с hello Azure CLI"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a>Управление виртуальными сетями Azure и виртуальных машин Linux с hello Azure CLI

Виртуальные машины Azure осуществляют внутреннее и внешнее взаимодействие через сеть Azure. В этом руководстве содержатся сведения о развертывании двух виртуальных машин и настройке для них сети Azure. Hello в примерах этого учебника предполагается, что виртуальные машины hello размещается веб-приложение с базы данных серверной части, однако приложение не развертывается в учебнике hello. Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * развернуть виртуальную сеть;
> * создавать подсеть в виртуальной сети;
> * Подключите виртуальные машины tooa подсети
> * управлять общедоступными IP-адресами виртуальной машины;
> * защищать входящий интернет-трафик;
> * Защита виртуальной Машины tooVM трафика


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="vm-networking-overview"></a>Обзор сети виртуальной машины

Виртуальные сети Azure включить безопасные сетевые подключения между виртуальными машинами, hello Интернета и других служб Azure, таких как базы данных Azure SQL. Виртуальные сети разбиты на логические сегменты — подсети. Используются подсети toocontrol сетевой поток и в качестве границы безопасности. При развертывании виртуальной Машины, обычно содержат виртуального сетевого интерфейса, подключенных tooa подсеть.

## <a name="deploy-virtual-network"></a>Развертывание виртуальной сети

В этом руководстве создается виртуальная сеть с двумя подсетями: интерфейсная подсеть для размещения веб-приложения и внутренняя подсеть для размещения сервера базы данных.

Прежде чем создать виртуальную сеть, выполните команду [az group create](/cli/azure/group#create), чтобы создать группу ресурсов. Hello следующий пример создает группу ресурсов с именем *myRGNetwork* в расположении eastus hello.

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a>Создание виртуальной сети

Здравствуйте, нам [создания az сети vnet](/cli/azure/network/vnet#create) toocreate команда виртуальной сети. В этом примере hello сети называется *mvVnet* и задан префикс адреса *10.0.0.0/16*. а также подсеть *mySubnetFrontEnd* с префиксом *10.0.1.0/24*. Далее в этом учебнике переднего плана виртуальная машина является подключенных toothis подсети. 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a>Создание подсети

Новая подсеть добавляется toohello виртуальной сети с помощью hello [создать подсеть виртуальной сети сети az](/cli/azure/network/vnet/subnet#create) команды. В этом примере hello подсеть с именем *mySubnetBackEnd* и задан префикс адреса *10.0.2.0/24*. Она используется со всеми внутренними службами.

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

На этом этапе мы создали сеть и разбили ее на две подсети — одна для интерфейсных служб, а вторая для внутренних служб. В следующем разделе hello виртуальные машины создаются и подключенных toothese подсетей.

## <a name="understand-public-ip-address"></a>Общие сведения об общедоступном IP-адресе

Общедоступный IP-адрес позволяет toobe ресурсы Azure доступны на hello Интернета. В этом разделе учебника hello виртуальной Машины создается toodemonstrate как toowork с общедоступным IP-адресов.

### <a name="allocation-method"></a>Способ выделения

Общедоступный IP-адрес может быть динамическим или статическим. По умолчанию выделяется динамический общедоступный IP-адрес. После освобождения виртуальной машины освобождаются также и динамические IP-адреса. Это приводит к возникновению hello IP адрес toochange во время любой операции, которая включает в себя освобождения виртуальной Машины.

метод распределения Hello можно задать toostatic, гарантирует, что IP-адрес hello остаются назначенный tooa виртуальной Машины, даже во время освобождена состояния. При использовании статически выделенный IP-адрес, hello IP-адрес не указан. Он выделяется из пула доступных адресов.

### <a name="dynamic-allocation"></a>Динамическое выделение

При создании виртуальной Машины с помощью hello [создания виртуальной машины az](/cli/azure/vm#create) команды выделения способ hello по умолчанию открытый IP-адреса является динамическим. В следующем примере hello виртуальная машина создается с динамический IP-адрес. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a>Статическое выделение

При создании виртуальной машины, с помощью hello [создания виртуальной машины az](/cli/azure/vm#create) , укажите hello `--public-ip-address-allocation static` tooassign аргумент статический общедоступный IP-адрес. Эта операция не рассматривается в этом учебнике, однако в следующем разделе hello динамически выделенный IP-адрес измененные tooa статически выделяется адрес. 

### <a name="change-allocation-method"></a>Изменение метода выделения

можно изменить способ распределения Hello IP-адреса с помощью hello [обновления открытого ip-сети az](/cli/azure/network/public-ip#update) команды. В этом примере hello способ выделения IP-адреса из интерфейса ВМ изменяется hello toostatic.

Во-первых освобождается hello виртуальной Машины.

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

Используйте hello [обновления открытого ip-сети az](/cli/azure/network/public-ip#update) команды tooupdate способ распределения hello. В этом случае hello `--allocation-method` задано слишком*статических*.

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

Запустите hello виртуальной Машины.

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a>Создание виртуальной машины без общедоступного IP-адреса

Часто, виртуальная машина не обязательно toobe доступно по Интернету hello. toocreate виртуальной Машины без общедоступный IP-адрес, используйте hello `--public-ip-address ""` аргумент с пустой набор двойных кавычек. Эта конфигурация рассматривается далее в этом руководстве.

## <a name="secure-network-traffic"></a>защищают сетевой трафик;

Группа безопасности сети (NSG) содержит список правил безопасности, которые разрешают или запрещают tooresources сетевого трафика, подключенных tooAzure виртуальных сетей (VNet). Nsg может быть связан toosubnets или отдельных сетевых интерфейсов. Когда NSG связана с сетевым интерфейсом, оно применяется только для hello связанных виртуальных Машин. Когда NSG связанные tooa подсети, hello правила применяются tooall ресурсы подключенных toohello подсети. 

### <a name="network-security-group-rules"></a>Правила группы безопасности сети

Правила группы безопасности сети определяют сетевые порты, через которые разрешен или запрещен трафик. Hello правила могут включать исходный и конечный диапазоны IP-адресов, так что трафик контролируется между определенными системами или подсети. Правилам также присваивается приоритет (от 1 до 4096), Правила, вычисляются в порядке приоритета hello. Правило с приоритетом 100 оценивается перед правилом с приоритетом 200.

Все группы NSG содержат набор правил по умолчанию. правила по умолчанию Hello не может быть удалена, но так как они будут назначены hello самый низкий приоритет, они могут быть переопределены созданных вами правил hello.

- **Виртуальная сеть.** Входящий и исходящий трафик виртуальной сети разрешен в обоих направлениях.
- **Интернет.** Исходящий трафик разрешен, но входящий трафик заблокирован.
- **Подсистема балансировки нагрузки** -работоспособности hello tooprobe подсистемы балансировки нагрузки Azure разрешить виртуальных машин и экземпляров ролей. Если набор балансировки нагрузки не используется, это правило можно переопределить.

### <a name="create-network-security-groups"></a>Создание групп безопасности сети

Группы безопасности могут быть созданы на hello же время, что и ВМ с помощью hello [создания виртуальной машины az](/cli/azure/vm#create) команды. При этом hello NSG связан с сетевым интерфейсом hello виртуальных машин и правило NSG является созданы автоматически tooallow трафик через порт *22* из любого источника. Ранее в этом учебнике приветствия переднего плана NSG был автоматически создан с hello интерфейса виртуальной Машины. Кроме того, было также создано правило NSG для порта 22. 

В некоторых случаях может быть полезным toopre-создать NSG, например, когда не следует создавать правила по умолчанию SSH или когда hello NSG должно быть вложенных tooa подсети. 

Используйте hello [создать az сети nsg](/cli/azure/network/nsg#create) toocreate команда группы безопасности сети.

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

Вместо того чтобы сопоставлять hello NSG tooa сетевого интерфейса, связанного с подсетью. В этой конфигурации все виртуальные Машины, вложенные toohello подсети наследует правила NSG hello.

Обновление существующей подсети hello с именем *mySubnetBackEnd* с новой NSG hello.

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

Теперь создайте виртуальную машину, являющийся вложенного toohello *mySubnetBackEnd*. Обратите внимание, что hello `--nsg` аргумент имеет значение пустой двойных кавычек. NSG не обязательно toobe, созданных с помощью hello виртуальной Машины. Hello виртуальной Машины — вложенное toohello конечной подсети защищены с помощью предварительно созданного внутреннего интерфейса NSG hello. Этот NSG применяется toohello виртуальной Машины. Кроме того, обратите внимание, что hello `--public-ip-address` аргумент имеет значение пустой двойных кавычек. Эта конфигурация создает виртуальную машину без общедоступного IP-адреса. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a>Защита входящего трафика

Когда hello интерфейса виртуальной Машины была создана, tooallow входящий трафик через порт 22 было создано правило NSG. Это правило позволяет toohello подключений SSH виртуальной Машины. В этом примере трафик также необходимо разрешить через порт *80*. Эта конфигурация обеспечивает toobe приложения web, доступе к hello виртуальной Машины.

Используйте hello [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) toocreate команда правило для порта *80*.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

Hello интерфейса виртуальной Машины, теперь доступны только через порт *22* и порт *80*. Весь входящий трафик блокируется в группы безопасности сети hello. Может оказаться полезным toovisualize hello NSG правила конфигурации. Конфигурация правила NSG возвращаемого hello с hello [список правил сетевой az](/cli/azure/network/nsg/rule#list) команды. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

Выходные данные:

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a>Защита виртуальной Машины tooVM трафика

Правила группы безопасности сети также можно применить между виртуальными машинами. В этом примере hello интерфейса виртуальной Машины требуется toocommunicate с hello внутренней виртуальной Машины на порте *22* и *3306*. Эта конфигурация позволяет соединений по протоколу SSH с hello интерфейса виртуальной Машины, а также позволяют приложению на hello переднего плана toocommunicate ВМ с внутренней базой данных MySQL. Должно быть заблокировано весь трафик между виртуальными машинами hello внешнего и внутреннего интерфейса.

Используйте hello [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) toocreate команда правило для порта 22. Обратите внимание, что hello `--source-address-prefix` аргумент задает значение *10.0.1.0/24*. Эта конфигурация гарантирует, что только из интерфейса подсети hello-трафика через hello NSG.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

Теперь добавьте правило, разрешающее трафик MySQL через порт 3306.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

Наконец, если у Nsg правило по умолчанию, что позволяет весь трафик между виртуальными машинами в hello же виртуальной сети, правила могут быть созданы для hello серверной части Nsg tooblock весь трафик. Обратите внимание, что hello `--priority` присваивается значение *300*, который меньше, что оба hello правила NSG и MySQL. Эта конфигурация гарантирует, что SSH и MySQL по-прежнему трафик через hello NSG.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

Hello внутренней виртуальной Машины, теперь доступны только через порт *22* и порт *3306* из интерфейса подсети hello. Весь входящий трафик блокируется в группы безопасности сети hello. Может оказаться полезным toovisualize hello NSG правила конфигурации. Конфигурация правила NSG возвращаемого hello с hello [список правил сетевой az](/cli/azure/network/nsg/rule#list) команды. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

Выходные данные:

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике создается и защищенных сетей Azure как связанные toovirtual машины. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * развертывать виртуальную сеть;
> * создавать подсеть в виртуальной сети;
> * Подключите виртуальные машины tooa подсети
> * управлять общедоступными IP-адресами виртуальной машины;
> * защищать входящий интернет-трафик;
> * Защита виртуальной Машины tooVM трафика

Переместить следующий учебник toolearn toohello о защите данных на виртуальных машинах с помощью резервного копирования Azure. 

> [!div class="nextstepaction"]
> [Архивация виртуальных машин Linux в Azure](./tutorial-backup-vms.md)
