---
title: "Здравствуйте, aaaControl маршрутизации и виртуальных устройств с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocontrol маршрутизации и виртуальных устройств с помощью hello Azure CLI 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a>Создайте маршруты определяемые пользователем (UDR) с помощью hello Azure CLI 1.0

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Интерфейс командной строки Azure](virtual-network-create-udr-arm-cli.md)
> * [Шаблон](virtual-network-create-udr-arm-template.md)
> * [PowerShell (классическая модель)](virtual-network-create-udr-classic-ps.md)
> * [Интерфейс командной строки (классическая модель)](virtual-network-create-udr-classic-cli.md)

Создание пользовательских маршрутизации и виртуальных устройств с помощью hello Azure CLI.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI 

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello. 

- [Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан на основании hello сценарии выше. Toorun hello команд, отображаемых в этом документе, сначала построения необходимо hello тестовой среды, развернув [этот шаблон](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello При необходимости и выполнения инструкции hello в hello портала.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Создать hello UDR для интерфейса подсети hello
Таблица маршрутов toocreate hello и маршрутов для подсети hello переднего плана, в зависимости от варианта hello выше, выполните следующие шаги hello.

1. Выполните следующие команды toocreate hello таблицы маршрутов для подсети интерфейса hello:

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    Выходные данные:
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    Параметры
   
   * **-g (или --resource-group)**. Имя группы ресурсов hello, где будут создаваться hello UDR. В данном сценарии это *TestRG*.
   * **-l (или --location)**. Регион Azure, где hello новый UDR будет создан. В нашем случае это *westus*.
   * **-n (или --name)**. Имя для hello новый UDR. В данном сценарии это *UDR-FrontEnd*.
2. Запустите все toohello внутренней подсети (192.168.2.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    Выходные данные:
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    Параметры
   
   * **-r (или --route-table-name)**. Имя таблицы маршрутов hello, куда будут добавлены hello маршрута. В данном сценарии это *UDR-FrontEnd*.
   * **-a (или --address-prefix)**. Префикс адреса для подсети hello, где пакеты, предназначенные для. В данном сценарии это *192.168.2.0/24*.
   * **-y (или --next-hop-type)**. Тип объекта, куда будет отправляться трафик. Возможные значения: *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* или *None*.
   * **-p (или --next-hop-ip-address**). IP-адрес следующего прыжка. В нашем случае это *192.168.0.4*.
3. Выполнения hello следующая команда созданную с hello таблицу маршрутов hello tooassociate **переднего плана** подсети:

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Выходные данные:
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    Параметры
   
   * **-e (или --vnet-name)**. Имя виртуальной сети, где находится подсети hello hello. В данном сценарии это *TestVNet*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Создать hello UDR для hello внутренней подсети
toocreate hello таблицы маршрутов и маршрутизации для подсети hello серверной части, в зависимости от варианта hello выше завершения hello, следующие шаги:

1. Выполните следующие команды toocreate hello таблицы маршрутов для подсети внутренней hello:

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. Запустите все toohello интерфейса подсети (192.168.1.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. Выполнения hello следующие таблицы маршрутов hello tooassociate команды с hello **серверной** подсети:

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>Включение IP-пересылки на FW1
tooenable IP-пересылки в hello сетевой Адаптер, используемый с **FW1**полный hello следующие действия:

1. Выполните команду hello, которое следует и обратите внимание, значение hello **включить IP-пересылки**. Оно должно быть задано слишком*false*.

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    Выходные данные:
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. Выполните следующие команды tooenable IP-пересылки hello.

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    Выходные данные:
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    Параметры
   
   * **-f (или --enable-ip-forwarding)**. Значение *true* или *false*.

