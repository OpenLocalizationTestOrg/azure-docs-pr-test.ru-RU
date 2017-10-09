---
title: "Виртуальная сеть — Azure CLI 2.0 aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной сети с помощью hello Azure CLI 2.0."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a>Создание виртуальной сети с помощью Azure CLI 2.0 hello

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую. Корпорация Майкрософт рекомендует создать ресурсы с помощью модели развертывания диспетчера ресурсов hello. Дополнительные сведения о toolearn hello различий между моделями hello двух чтения hello [модели развертывания Azure понять](../azure-resource-manager/resource-manager-deployment-model.md) статьи.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления
- [Azure CLI 2.0](#create-a-virtual-network) -нашей нового поколения CLI для модели развертывания управления hello ресурсов (в этой статье) "
 
    Также можно создать виртуальную сеть через диспетчер ресурсов с помощью других средств или создайте виртуальную сеть через hello классической модели развертывания, выбрав другой вариант hello после списка:

> [!div class="op_single_selector"]
> * [Портал](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-networks-create-vnet-arm-cli.md)
> * [Шаблон](virtual-networks-create-vnet-arm-template-click.md)
> * [Портал (классический)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (классическая модель)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [Интерфейс командной строки (классическая модель)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a>Создать виртуальную сеть

в виртуальной сети с помощью toocreate hello Azure CLI 2.0 завершения hello, следующие шаги:

1. Установка и настройка hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

2. Создание группы ресурсов для виртуальной сети с помощью hello [Создание группы az](/cli/azure/group#create) с hello `--name` и `--location` аргументов:

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. Создайте виртуальную сеть и подсеть.

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    Ожидаемые выходные данные:
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    Используемые параметры:

    - `--name TestVNet`: Имя toobe виртуальной сети hello создан.
    - `--resource-group TestRG`: имя группы ресурсов hello #, управляющий hello ресурсов. 
    - `--location centralus`: hello расположение, в которой toodeploy.
    - `--address-prefix 192.168.0.0/16`: hello префикс адреса и блока.  
    - `--subnet-name FrontEnd`: имя подсети hello hello.
    - `--subnet-prefix 192.168.1.0/24`: hello префикс адреса и блока.

    toolist toouse основные сведения hello в hello Далее команды можно запросить с помощью виртуальной сети hello [фильтр запроса](/cli/azure/query-az-cli2):

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    Что порождает hello следующие выходные данные:

        Where      Name      Group

        centralus  TestVNet  TestRG

4. Создайте подсеть.

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    Ожидаемые выходные данные:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    Используемые параметры:

    - `--address-prefix 192.168.2.0/24`: блок CIDR подсети.
    - `--name BackEnd`: Имя hello новую подсеть.
    - `--resource-group TestRG`: hello группы ресурсов.
    - `--vnet-name TestVNet`: имя hello hello, которой принадлежит виртуальной сети.

5. Свойства запроса hello hello новой виртуальной сети:

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    Ожидаемые выходные данные:

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. Свойства запроса hello hello подсетей:

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    Ожидаемые выходные данные:

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как tooconnect:

- Виртуальная сеть виртуальной машины (VM) tooa, считывая hello [создания виртуальной Машины Linux](../virtual-machines/linux/quick-create-cli.md) статьи. Вместо создания виртуальной сети и подсети в шагах hello hello статей, можно выбрать существующей виртуальной сети и подсети tooconnect для виртуальной Машины.
- Здравствуйте, считывая hello виртуальных сетей в виртуальной сети tooother [подключение виртуальных сетей](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) статьи.
- tooan Hello виртуальной сети в локальной сети с помощью виртуальной частной сети сеть сеть (VPN) или канал ExpressRoute. Дополнительные сведения в разделе hello [подключения локальной сети tooan виртуальной сети с помощью VPN сайтами](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) и [связывание виртуальной сети tooan канал ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
