---
title: "aaaConfigure частных IP-адресов для виртуальных машин - CLI Azure 2.0 | Документы Microsoft"
description: "Узнайте, как tooconfigure частных IP-адресов для виртуальных машин с помощью hello Azure командной строки (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a>Настройка частного IP-адреса для виртуальной машины с помощью Azure CLI 2.0 hello

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI 

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello. 

- [Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления 
- [Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -нашей нового поколения CLI для модели развертывания управления hello ресурсов (в этой статье)

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello модели развертывания диспетчера ресурсов. Вы также можете [управление статический частный IP-адрес в hello классической модели развертывания](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> приведенную ниже команду CLI Azure 2.0 Образец Hello ожидать простой среде уже создан. Если требуется toorun hello команд, отображаемых в этом документе, вначале построить hello тестовой среды, описанные в [создании виртуальной сети](virtual-networks-create-vnet-arm-cli.md).

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a>Указание статического частного IP-адреса при создании виртуальной машины

toocreate Виртуальную машину с именем *DNS01* в hello *переднего плана* подсети виртуальной сети с именем *TestVNet* с статических частного IP-адреса *192.168.1.101*, выполните следующие действия hello.

1. Если еще не еще, установить и настроить hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login). 

2. Создать общедоступный IP-адрес для hello виртуальной Машины с hello [создать az сетевого public-IP-адреса](/cli/azure/network/public-ip#create) команды. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.

    > [!NOTE]
    > Возможно или toouse различные значения для аргументов, в этом и последующих шагов в зависимости от среды.
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    Ожидаемые выходные данные:
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * `--resource-group`: Имя группы ресурсов hello в какие toocreate hello общедоступный IP-адрес.
   * `--name`: Имя hello общедоступный IP-адрес.
   * `--location`: Azure область какие toocreate hello общедоступный IP-адрес.

3. Запустите hello [сетевого адаптера сети az создать](/cli/azure/network/nic#create) команда toocreate сетевой Адаптер с статический частных IP-адрес. Список Hello отображаться после вывода hello объясняется hello параметров, используемых. 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    Ожидаемые выходные данные:
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    Параметры

    * `--private-ip-address`: Статический частный IP-адрес для hello сетевого адаптера.
    * `--vnet-name`: Имя hello виртуальной сети, в которой toocreate hello сетевого адаптера.
    * `--subnet`: Имя hello подсети, в которой toocreate hello сетевого адаптера.

4. Запустите hello [создания виртуальной машины azure](/cli/azure/vm/nic#create) команда toocreate hello созданную виртуальную Машину с помощью hello общедоступного IP-адреса и сетевого Адаптера. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    Ожидаемые выходные данные:
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   Параметры, кроме hello basic [создания виртуальной машины az](/cli/azure/vm#create) параметров.

   * `--nics`: Имя hello toowhich hello сетевого Адаптера виртуальной Машины она будет присоединена.
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a>Получение сведений о статическом частном IP-адресе виртуальной машины

tooview hello статический частный IP-адрес, созданный, запустите следующую команду Azure CLI hello и просмотрите значения hello *метод alloc частный IP-адрес* и *частный IP-адрес*:

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

Ожидаемые выходные данные:

```json
"192.168.1.101"
```

toodisplay специально hello IP подробности hello сетевой Адаптер для этой виртуальной Машины, запрос hello сетевого Адаптера:

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

выходные данные Hello выглядят примерно так:

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a>Удаление статического частного IP-адреса виртуальной машины

Статический частный IP-адрес нельзя удалить из сетевой карты с использованием Azure CLI для развертываний Resource Manager. Необходимо следующее:
- Создайте сетевую карту, использующую динамический IP-адрес.
- Задать hello сетевого Адаптера виртуальной Машины hello hello вновь созданные сетевого адаптера. 

hello toochange сетевого Адаптера для hello виртуальной Машины, используемой в командах hello выше, выполните шаги hello.

1. Запустите hello **сетевого адаптера сети azure создать** команды toocreate новый сетевой Адаптер, с помощью динамического выделения IP-адресов с помощью нового IP-адреса. Обратите внимание, что поскольку IP-адрес не указан, способ распределения hello **динамическое**.

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    Ожидаемые выходные данные:

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. Запустите hello **набор виртуальных машин azure** команда toochange hello сетевой Адаптер, используемый hello виртуальной Машины.
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    Ожидаемые выходные данные:
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > Если hello виртуальной Машины достаточно большой toohave более одного сетевого Адаптера, запустите hello **удалить сетевого адаптера сети azure** команды toodelete, старый hello сетевого адаптера.
   
## <a name="next-steps"></a>Дальнейшие действия
* Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .
* Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).

