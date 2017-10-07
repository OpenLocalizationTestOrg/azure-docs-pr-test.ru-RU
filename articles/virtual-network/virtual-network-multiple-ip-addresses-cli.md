---
title: "aaaVM несколько IP-адресов с помощью Azure CLI 2.0 hello | Документы Microsoft"
description: "Узнайте, как tooassign несколько IP-адресов tooa виртуальную машину с помощью Azure CLI 2.0 \"hello\" | Диспетчер ресурсов."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a>Назначить несколько IP-адресов машин toovirtual, с помощью Azure CLI 2.0 hello

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

В этой статье объясняется, как toocreate виртуальной машины (VM) с помощью hello Azure Resource Manager развертывания модели с помощью hello Azure CLI 2.0. Несколько IP-адресов нельзя назначить tooresources, созданные с помощью hello классической модели развертывания. Дополнительные сведения о моделях развертывания Azure, чтение hello toolearn [понять модели развертывания](../resource-manager-deployment-model.md) статьи.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Создание виртуальной машины с несколькими IP-адресами

Выполнить эту задачу с помощью hello Azure CLI 2.0 (Эта статья) или hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md). Измените значения hello, в зависимости от среды. Привет, описанных ниже объясняется, как toocreate пример виртуальной Машины с несколькими IP-адресов, как описано в сценарии hello. Измените имена переменных в прямых кавычках и типы IP-адресов в соответствии с требованиями своей реализации. 

1. Установка hello [Azure CLI 2.0](/cli/azure/install-az-cli2) если его нет.
2. Создание открытого и закрытого пару ключей SSH для виртуальных машин Linux, выполнив шаги hello в hello [создать открытый и закрытый пару ключей SSH для виртуальных машин Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. В командной оболочке входа с помощью команды hello `az login` и выберите hello подписку, которую вы используете.
4. Создайте hello виртуальной Машины, выполнив скрипт hello на компьютере Mac или Linux. Hello скрипт создает группу ресурсов, одной виртуальной сети (VNet), один сетевой Адаптер с тремя IP-конфигурации и виртуальной Машины с tooit hello двух сетевых адаптеров присоединен. Здравствуйте, сетевой Адаптер, общедоступный IP-адрес, виртуальной сети и ресурсы виртуальной Машины должны существовать в hello же местоположение и подписку. Хотя ресурсы hello все еще нет tooexist в hello одну группу ресурсов, в следующий сценарий, как и hello.

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

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
```

В дополнение к этому toocreating ВМ с сетевой КАРТОЙ с 3 IP-конфигурации hello скрипт создает:

- Один premium управлять диска по умолчанию, но наличия других параметров для hello тип диска, которые можно создать. Чтение hello [создания ВМ Linux с помощью Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Дополнительные сведения см.
- Виртуальная сеть с одной подсетью и двумя общедоступными IP-адресами. Кроме того, можно использовать *имеющиеся* виртуальные сети, подсети, сетевые карты или общедоступные IP-адреса. toolearn как toouse существующие сетевые ресурсы, вместо создания дополнительных ресурсов, введите `az vm create -h`.

За общедоступные IP-адреса взимается номинальная плата. Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы. Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке. Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.

После создания виртуальной Машины hello введите hello `az network nic show --name MyNic1 --resource-group myResourceGroup` конфигурацию сетевого Адаптера hello tooview команды. Введите hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview список IP-конфигурации hello связанные toohello сетевого адаптера.

Добавить hello частного IP адресов toohello ВМ операционной системы, выполнив шаги hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи.

## <a name="add"></a>Добавьте IP адресов tooa виртуальной Машины

Можно добавить дополнительные частных и общедоступных IP адресов tooan существующего сетевого Адаптера, выполнив hello, описанных ниже. Hello примеры созданы на основе hello [сценарий](#Scenario) описано в этой статье.

1. Откройте командную строку и завершения hello оставшиеся шаги в этом разделе в одном сеансе. Если у вас еще нет Azure CLI установлен и настроен, hello завершения шагов в hello [установки Azure CLI 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour статьи и входа учетная запись Azure с hello `az-login` команды.

2. Выполните действия hello в одном из следующих разделах, в зависимости от требований hello.

    **Добавление частного IP-адреса**
    
    tooadd закрытый tooa адрес IP сетевого Адаптера, необходимо создать IP-конфигурации, с помощью команды hello ниже. Hello статический IP-адрес должен быть неиспользуемый адрес для подсети hello.

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    Вы можете создать любое количество конфигураций, указывая для них уникальные имена и уникальные частные IP-адреса (если используются статические IP-адреса).

    **Добавление общедоступного IP-адреса**
    
    Общедоступный IP-адрес будет добавлен, связав ее tooeither новой конфигурации IP или существующей конфигурации IP. Этапы hello в одном hello следующих разделах, сколько требуется.

    За общедоступные IP-адреса взимается номинальная плата. Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы. Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке. Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.

    - **Связать новую конфигурацию IP hello ресурсов tooa**
    
        Чтобы добавить общедоступный IP-адрес в новую IP-конфигурацию, необходимо добавить и частный IP-адрес, так как все IP-конфигурации должны иметь частный IP-адрес. В конфигурацию можно добавить имеющийся ресурс общедоступного IP-адреса или создать новый. toocreate новый, введите следующую команду hello:
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        toocreate новой конфигурации IP с статический частный IP-адрес и связанные hello *myPublicIP3* общедоступный IP-адрес адрес ресурса, введите следующую команду hello:

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - **Существующую конфигурацию IP связан hello ресурсов tooan** открытого ресурса IP-адреса можно только связанные tooan IP-конфигурации, уже не связан. Можно определить, имеет ли связанный общий IP-адрес IP-адрес, введя следующую команду hello.

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        Возвращаемые выходные данные:
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        С момента hello **PublicIpAddressId** столбца для *IpConfig 3* является пустым в hello выходные данные, не открытого ресурса IP-адреса является в настоящее время связаны tooit. Можно добавить существующие открытый IP адрес ресурса tooIpConfig-3, или введите hello, следующая команда toocreate один:

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        Введите следующую команду, общедоступный IP-адрес tooassociate hello адресов toohello существующие IP конфигурации ресурса с именем hello *IPConfig 3*:
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. Представление hello частных IP-адресов и hello открытый IP-адресов идентификаторы ресурсов, назначенных toohello hello сетевого Адаптера, введя следующую команду:

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    Возвращаемые выходные данные: <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. Добавить hello частных IP-адресов вы добавили операционной системы ВМ toohello toohello сетевой Адаптер, следуя инструкциям hello hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи. Не добавляйте hello открытый IP адресов toohello операционной системы.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
