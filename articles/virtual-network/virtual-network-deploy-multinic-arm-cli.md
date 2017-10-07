---
title: "виртуальную Машину с несколькими сетевыми картами - CLI Azure 2.0 aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной Машины с несколькими сетевыми картами с помощью hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a>Создайте виртуальную Машину с несколькими сетевыми адаптерами, используя hello Azure CLI 2.0

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).  В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](virtual-network-deploy-multinic-classic-cli.md).
>

## <a name="create"></a>Создание виртуальной Машины hello

Выполнить эту задачу с помощью hello Azure CLI 2.0 (Эта статья) или hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md). Здравствуйте, значения в «» для переменных hello в hello описанных ниже создать ресурсы с параметрами из сценария hello. Измените значения hello, в зависимости от среды.

1. Установка hello [Azure CLI 2.0](/cli/azure/install-az-cli2) если его нет.
2. Создание открытого и закрытого пару ключей SSH для виртуальных машин Linux, выполнив шаги hello в hello [создать открытый и закрытый пару ключей SSH для виртуальных машин Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. В командной оболочке входа с помощью команды hello `az login`.
4. Создайте hello виртуальной Машины, выполнив скрипт hello на компьютере Mac или Linux. Hello скрипт создает группу ресурсов tooit присоединенного одной виртуальной сети (VNet) с двумя подсетями, двумя сетевыми адаптерами и виртуальной Машины с hello двух сетевых адаптеров. Одно из hello сетевых адаптеров — подключенных tooone подсети и присваивается статический IP-адрес открытого и закрытого. Hello другой сетевой Адаптер имеет подключенного toohello другие подсети и назначается статический частный IP-адрес, а не общедоступный IP-адрес. Здравствуйте, сетевой Адаптер, общедоступный IP-адрес, виртуальной сети и ресурсы виртуальной Машины должны существовать в hello же местоположение и подписку. Хотя ресурсы hello все еще нет tooexist в hello одну группу ресурсов, в следующий сценарий, как и hello.

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

В дополнение к этому toocreating ВМ с двумя сетевыми адаптерами hello скрипт создает:
- Один premium управлять диска по умолчанию, но наличия других параметров для hello тип диска, которые можно создать. Чтение hello [создания ВМ Linux с помощью Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Дополнительные сведения см.
- Виртуальная сеть с двумя подсетями и одним общедоступным IP-адресом. Кроме того, можно использовать *имеющиеся* виртуальные сети, подсети, сетевые карты или общедоступные IP-адреса. toolearn как toouse существующие сетевые ресурсы, вместо создания дополнительных ресурсов, введите `az vm create -h`.

## <a name = "validate"></a>Проверка создания виртуальной машины и сетевых карт

1. Введите команду hello `az resource list --resouce-group Multi-NIC-VM --output table` toosee список ресурсов hello создан с помощью сценария hello. В выходные данные возвращаются hello должно быть шесть ресурсы: два сетевых адаптера, один диск, общедоступный IP-адрес, одну виртуальную сеть и виртуальную машину.
2. Введите команду hello `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`. Выходные данные возвращаются hello, обратите внимание, в значение hello **IP-адрес** и что значение hello **PublicIpAllocationMethod** — *статических*.
3. Прежде чем запускать следующую команду hello, удалите hello <>, замените *Username* с именем hello, который использовался для hello **Username** переменной в скрипт hello и заменить *IP-адрес* с hello **IP-адрес** из предыдущего шага hello. Выполнения hello следующая команда tooconnect toohello виртуальной Машины: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 
4. После подключения toohello виртуальных Машин, запустите hello `sudo ifconfig` toosee команда *eth0* и *eth1* интерфейсов. Каждый сетевой Адаптер был присвоен hello статических частных IP-адресов указывается в скрипте hello hello Azure DHCP-серверами. Hello IP- и MAC адресов, назначенных toohello сетевых адаптеров не изменяйте до hello виртуальная машина удаляется. Рекомендуется не изменять IP-адреса в операционной системе, как его можно отключить компьютер toohello подключения. Общедоступные IP-адреса не отображаются в операционной системе hello, как они являются tooand сетевой адрес преобразуется из hello частный IP-адрес с hello инфраструктуры Azure.

## <a name= "clean-up"></a>Удалите hello ВМ и связанные ресурсы

Рекомендуется удалить hello ресурсы, созданные в этом упражнении, если не использовать их в рабочей среде. За виртуальную машину, общедоступный IP-адрес и диск взимается плата, пока они подготовлены. tooremove hello ресурсы, созданные во время этого упражнения завершения hello, следующие шаги:
1. tooview hello ресурсы в группе ресурсов hello, запустите hello `az resource list --resource-group Multi-NIC-VM` команды.
2. Убедитесь, что нет ресурсов в группе ресурсов hello, за исключением hello ресурсов создан с помощью сценария hello в этой статье. 
3. все ресурсы, созданные в этом упражнении запуска hello toodelete `az group delete --name Multi-NIC-VM` команды. Hello команда удаляет группу ресурсов hello и все ресурсы hello, содержащихся в нем.

## <a name="next-steps"></a>Дальнейшие действия

Любой сетевой трафик могут передаваться tooand из hello создания виртуальной Машины в этой статье. Можно определить правила входящих и исходящих подключений в NSG, ограничить объем трафика hello, который может осуществляться tooand из каждого сетевого интерфейса и/или в каждой подсети. Дополнительные сведения о Nsg, чтение hello toolearn [NSG Обзор](virtual-networks-nsg.md) статьи.
