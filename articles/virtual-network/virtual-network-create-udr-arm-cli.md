---
title: "Здравствуйте, aaaControl маршрутизации и виртуальных устройств с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Узнайте, как toocontrol маршрутизации и виртуальных устройств с помощью hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a>Создайте маршруты определяемые пользователем (UDR) с помощью Azure CLI 2.0 hello

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Интерфейс командной строки Azure](virtual-network-create-udr-arm-cli.md)
> * [Шаблон](virtual-network-create-udr-arm-template.md)
> * [PowerShell (классическое развертывание)](virtual-network-create-udr-classic-ps.md)
> * [Интерфейс командной строки (классическое развертывание)](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI 

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello. 

- [Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления 
- [Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -нашей нового поколения CLI для модели развертывания управления hello ресурсов (в этой статье)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан на основании hello сценарии выше. Toorun hello команд, отображаемых в этом документе, сначала построения необходимо hello тестовой среды, развернув [этот шаблон](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello При необходимости и выполнения инструкции hello в hello портала.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Создать hello UDR для интерфейса подсети hello
Таблица маршрутов toocreate hello и маршрутов для подсети hello переднего плана, в зависимости от варианта hello выше, выполните следующие шаги hello.

1. Создание таблицы маршрутов для подсети интерфейса hello с hello [создание таблицы маршрутов в сети az](/cli/azure/network/route-table#create) команды:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    Выходные данные:

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. Создать маршрут, который отправляет все toohello внутренней подсети (192.168.2.0/24) toohello трафика, предназначенного **FW1** виртуальную Машину (192.168.0.4) с помощью hello [создать маршрут к таблице маршрутов сети az](/cli/azure/network/route-table/route#create) команды:

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    Выходные данные:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    Параметры

    * **--route-table-name**. Имя таблицы маршрутов hello, куда будут добавлены hello маршрута. В данном сценарии это *UDR-FrontEnd*.
    * **--address-prefix**. Префикс адреса для подсети hello, где пакеты, предназначенные для. В данном сценарии это *192.168.2.0/24*.
    * **--next-hop-type**. Тип объекта, куда будет отправляться трафик. Возможные значения: *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* или *None*.
    * **--next-hop-ip-address**. IP-адрес следующего прыжка. В нашем случае это *192.168.0.4*.

3. Запустите hello [обновления подсети виртуальной сети сети az](/cli/azure/network/vnet/subnet#update) созданную таблицу маршрутов hello tooassociate команды с hello **переднего плана** подсети:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    Выходные данные:

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    Параметры
    
    * **--vnet-name**. Имя виртуальной сети, где находится подсети hello hello. В данном сценарии это *TestVNet*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Создать hello UDR для hello внутренней подсети

toocreate hello таблицы маршрутов и маршрутизации для подсети hello серверной части, в зависимости от варианта hello выше завершения hello, следующие шаги:

1. Выполните следующие команды toocreate hello таблицы маршрутов для подсети внутренней hello:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. Запустите все toohello интерфейса подсети (192.168.1.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. Выполнения hello следующие таблицы маршрутов hello tooassociate команды с hello **серверной** подсети:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>Включение IP-пересылки на FW1

tooenable IP-пересылки в hello сетевой Адаптер, используемый с **FW1**полный hello следующие действия:

1. Запустите hello [Показать сетевого адаптера сети az](/cli/azure/network/nic#show) с toodisplay JMESPATH фильтра, hello текущей **включить пересылку ip** значение для **включить IP-пересылки**. Оно должно быть задано слишком*false*.

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    Выходные данные:

        false

2. Выполните следующие команды tooenable IP-пересылки hello.

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    Изучите консоли toohello потокового вывода hello или просто повторное тестирование для конкретных hello **enableIpForwarding** значение:

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    Выходные данные:

        true

    Параметры

    **--ip-forwarding**: *true* или *false*.

