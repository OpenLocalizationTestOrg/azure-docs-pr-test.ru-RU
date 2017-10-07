---
title: "aaaControl маршрутизации в классической виртуальной сети Azure - CLI - | Документы Microsoft"
description: "Узнайте, как toocontrol маршрутизации в виртуальных сетей с помощью hello Azure CLI в hello классической модели развертывания"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a>Маршрутизация управления и использования виртуальных устройств (классической) с помощью hello Azure CLI

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Интерфейс командной строки Azure](virtual-network-create-udr-arm-cli.md)
> * [Шаблон](virtual-network-create-udr-arm-template.md)
> * [PowerShell (классическая модель)](virtual-network-create-udr-classic-ps.md)
> * [Интерфейс командной строки (классическая модель)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello классической модели развертывания. Вы также можете [управлять маршрутизацией и использования виртуальных устройств в модели развертывания диспетчера ресурсов hello](virtual-network-create-udr-arm-cli.md).

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан на основании hello сценарии выше. Toorun hello команд, отображаемых в этом документе, создать среды hello, показанный на [Создание виртуальной сети (классические), с помощью Azure CLI hello](virtual-networks-create-vnet-classic-cli.md).

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Создать hello UDR для подсети hello переднего плана
Таблица маршрутов toocreate hello и маршрутов для подсети hello переднего плана, в зависимости от варианта hello выше, выполните следующие шаги hello.

1. Следующая команда tooswitch tooclassic режим выполнения hello:

    ```azurecli
    azure config mode asm
    ```

    Выходные данные:

        info:    New mode is asm

2. Выполните следующие команды toocreate hello таблицы маршрутов для подсети интерфейса hello:

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    Выходные данные:
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    Параметры
   
   * **-l (или --location)**. Регион Azure, где hello новой NSG будет создан. В нашем случае это *westus*.
   * **-n (или --name)**. Имя для hello новая NSG. В данном сценарии это *NSG-FrontEnd*.
3. Запустите все toohello внутренней подсети (192.168.2.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    Выходные данные:
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    Параметры
   
   * **-r (или --route-table-name)**. Имя таблицы маршрутов hello, куда будут добавлены hello маршрута. В данном сценарии это *UDR-FrontEnd*.
   * **-a (или --address-prefix)**. Префикс адреса для подсети hello, где пакеты, предназначенные для. В данном сценарии это *192.168.2.0/24*.
   * **-t (или --next-hop-type)**. Тип объекта, куда будет отправляться трафик. Возможные значения: *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* или *None*.
   * **-p (или --next-hop-ip-address**). IP-адрес следующего прыжка. В нашем случае это *192.168.0.4*.
4. Выполнения hello следующая команда таблицы маршрутов hello tooassociate, созданных с помощью hello **переднего плана** подсети:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Выходные данные:
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    Параметры
   
   * **-t (или --vnet-name)**. Имя виртуальной сети, где находится подсети hello hello. В данном сценарии это *TestVNet*.
   * **-n (или --subnet-name**). Имя таблицы маршрутов hello hello подсеть будет добавлено к. В данном сценарии это *FrontEnd*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Создать hello UDR для hello внутренней подсети
Таблица маршрутов toocreate hello и маршрута, необходимые для hello конечной подсети в зависимости от варианта hello, полный hello, следующие шаги:

1. Выполните следующие команды toocreate hello таблицы маршрутов для подсети внутренней hello:

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. Запустите все toohello интерфейса подсети (192.168.1.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. Выполнения hello следующие таблицы маршрутов hello tooassociate команды с hello **серверной** подсети:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

