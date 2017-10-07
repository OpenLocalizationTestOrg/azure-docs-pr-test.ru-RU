---
title: "aaaCreate сетевых групп безопасности - CLI Azure 2.0 | Документы Microsoft"
description: "Узнайте, как toocreate и развертывание сетевых групп безопасности с помощью Azure CLI 2.0 hello."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a>Создание группы безопасности с помощью Azure CLI 2.0 hello сети

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI 

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello. 

- [Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления 
- [Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -нашей нового поколения CLI для модели развертывания управления hello ресурсов (в этой статье)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Образец Hello Azure CLI 2.0 команды ниже ожидать простой среде уже создан на основании предыдущего сценария hello. 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a>Создать hello NSG для hello `FrontEnd` подсети

toocreate NSG с именем *NSG-FrontEnd* в зависимости от предыдущего сценария hello, выполните следующие шаги hello.

1. Если еще не еще, установить и настроить hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login). 

2. Создание с помощью hello NSG [создать az сети nsg](/cli/azure/network/nsg#create) команды. 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    Параметры
   
   * `--resource-group`: Имя группы ресурсов hello, где создается hello NSG. В данном сценарии это *TestRG*.
   * `--location`: Azure регион, где hello новой NSG создается. В нашем случае это *westus*.
   * `--name`: Имя hello новая NSG. В данном сценарии это *NSG-FrontEnd*.

    Hello тесты на ожидаемые выходные данные выглядят бит сведения, включая список всех правил по умолчанию hello. Hello пример hello правила по умолчанию, с помощью фильтра запроса JMESPATH с hello `table` формат вывода:

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   Выходные данные:

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. Создать правило, разрешающее доступ tooport 3389 (RDP) из hello Интернета с hello [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) команды.

    > [!NOTE]
    > В зависимости от hello оболочки используется, может потребоваться toomodify hello `*` знаку в hello аргументы после так как не tooexpand hello аргумент перед выполнением.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    Ожидаемые выходные данные:
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    Параметры

    * `--resource-group testrg`: hello toouse группы ресурсов. Обратите внимание, что в ней не учитывается регистр.
    * `--nsg-name NSG-FrontEnd`: Имя hello NSG, в которой hello создается правило.
    * `--name rdp-rule`: Имя для нового правила hello.
    * `--access Allow`: Уровень доступа hello правила (запретить или разрешить).
    * `--protocol Tcp` — протокол (TCP, UDP или "*").
    * `--direction Inbound`: Направление соединения hello (входящий или исходящий).
    * `--priority 100`: Приоритет для правила hello.
    * `--source-address-prefix Internet` — префикс адреса источника в CIDR или использование тегов по умолчанию.
    * `--source-port-range "*"` — исходный порт или диапазон портов. Порт, который подключился hello.
    * `--destination-address-prefix "*"` — префикс адреса назначения в CIDR или использование тегов по умолчанию.
    * `--destination-port-range 3389` — конечный порт или диапазон портов. Порт, который получает запрос на подключение hello.



4. Создать правило, разрешающее доступ tooport 80 (HTTP) из Интернета hello **создать правило nsg сети az** команды.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    Ожидаемые выходные данные:
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. Привязать hello NSG toohello **переднего плана** подсети с hello [обновления подсети виртуальной сети сети az](/cli/azure/network/vnet/subnet#update) команды.
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    Ожидаемые выходные данные:
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a>Создать hello NSG для hello `BackEnd` подсети
toocreate NSG с именем *NSG серверной* в зависимости от предыдущего сценария hello, выполните следующие шаги hello.

1. Создать hello `NSG-BackEnd` NSG с **создать az сети nsg**.
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    Как на шаге 2 выше hello тесты на ожидаемые выходные данные довольно велик, включая правила по умолчанию.
   
2. Создать правило, разрешающее доступ tooport 1433 (SQL) из hello `FrontEnd` подсети с hello **создать правило nsg сети az** команды.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    Ожидаемые выходные данные:

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. Создать правило, запрещающее доступ toohello в Интернет с помощью hello **создать правило nsg сети az** команды.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    Ожидаемые выходные данные:
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. Привязать hello NSG toohello `BackEnd` подсеть, используя hello **набор подсети виртуальной сети сети az** команды.
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    Ожидаемые выходные данные:
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
