---
title: "aaaCreate виртуальную Машину с статический общедоступный IP-адрес - CLI Azure 2.0 | Документы Microsoft"
description: "Узнайте, как toocreate ВМ с статических открытый IP адрес с помощью hello Azure командной строки (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a>Создайте виртуальную Машину с помощью hello Azure CLI 2.0 статический общедоступный IP-адрес

> [!div class="op_single_selector"]
> * [Портал Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md)
> * [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [Шаблон](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (классическая модель)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name = "create"></a>Создание виртуальной Машины hello

Выполнить эту задачу с помощью hello Azure CLI 2.0 (Эта статья) или hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md). Здравствуйте, значения в «» для переменных hello в hello описанных ниже создать ресурсы с параметрами из сценария hello. Измените значения hello, в зависимости от среды.

1. Установка hello [Azure CLI 2.0](/cli/azure/install-az-cli2) если его нет.
2. Создание открытого и закрытого пару ключей SSH для виртуальных машин Linux, выполнив шаги hello в hello [создать открытый и закрытый пару ключей SSH для виртуальных машин Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. В командной оболочке входа с помощью команды hello `az login`.
4. Создайте hello виртуальной Машины, выполнив скрипт hello на компьютере Mac или Linux. Hello Azure общедоступный IP-адрес, виртуальная сеть, сетевой интерфейс и ресурсы виртуальной Машины должны существовать в hello же расположение. Хотя ресурсы hello все еще нет tooexist в hello одну группу ресурсов, в следующий сценарий, как и hello.

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

В дополнение к этому toocreating ВМ hello скрипт создает:
- Один premium управлять диска по умолчанию, но наличия других параметров для hello тип диска, которые можно создать. Чтение hello [создания ВМ Linux с помощью Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Дополнительные сведения см.
- Виртуальная сеть, подсеть, сетевая карта и общедоступный IP-адрес. Кроме того, можно использовать *имеющиеся* виртуальные сети, подсети, сетевые карты или общедоступные IP-адреса. toolearn как toouse существующие сетевые ресурсы, вместо создания дополнительных ресурсов, введите `az vm create -h`.

## <a name = "validate"></a>Проверка создания виртуальной машины и общедоступного IP-адреса

1. Введите команду hello `az resource list --resouce-group IaaSStory --output table` toosee список ресурсов hello создан с помощью сценария hello. В выходные данные возвращаются hello должно быть пять ресурсы: сетевого интерфейса, диск, общедоступный IP-адрес, виртуальной сети и виртуальной машины.
2. Введите команду hello `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`. Выходные данные возвращаются hello, обратите внимание, в значение hello **IP-адрес** и что значение hello **PublicIpAllocationMethod** — *статических*.
3. Перед выполнением hello следующую команду, удалите hello <>, замените *Username* с именем hello, который использовался для hello **Username** переменных в скрипт hello и заменить *IP-адрес* с hello **IP-адрес** из предыдущего шага hello. Выполнения hello следующая команда tooconnect toohello виртуальной Машины: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 

## <a name= "clean-up"></a>Удалите hello ВМ и связанные ресурсы

Рекомендуется удалить hello ресурсы, созданные в этом упражнении, если не использовать их в рабочей среде. За виртуальную машину, общедоступный IP-адрес и диск взимается плата, пока они подготовлены. tooremove hello ресурсы, созданные во время этого упражнения завершения hello, следующие шаги:

1. tooview hello ресурсы в группе ресурсов hello, запустите hello `az resource list --resource-group IaaSStory` команды.
2. Убедитесь, что нет ресурсов в группе ресурсов hello, за исключением hello ресурсов создан с помощью сценария hello в этой статье. 
3. все ресурсы, созданные в этом упражнении запуска hello toodelete `az group delete -n IaaSStory` команды. Hello команда удаляет группу ресурсов hello и все ресурсы hello, содержащихся в нем.

## <a name="next-steps"></a>Дальнейшие действия

Любой сетевой трафик могут передаваться tooand из hello создания виртуальной Машины в этой статье. Можно определить правила входящих и исходящих подключений в NSG, ограничить объем трафика hello, который может осуществляться tooand из сетевого интерфейса hello и подсети hello. Дополнительные сведения о Nsg, чтение hello toolearn [NSG Обзор](virtual-networks-nsg.md) статьи.
