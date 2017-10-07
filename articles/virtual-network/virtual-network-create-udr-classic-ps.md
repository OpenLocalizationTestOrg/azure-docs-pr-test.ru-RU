---
title: "aaaControl маршрутизации в классической виртуальной сети Azure - PowerShell - | Документы Microsoft"
description: "Узнайте, как toocontrol маршрутизации в виртуальных сетей с помощью PowerShell | Классический"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a>Управление маршрутизацией и использование виртуальных модулей (классический режим) с помощью PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Интерфейс командной строки Azure](virtual-network-create-udr-arm-cli.md)
> * [Шаблон](virtual-network-create-udr-arm-template.md)
> * [PowerShell (классическая модель)](virtual-network-create-udr-classic-ps.md)
> * [Интерфейс командной строки (классическая модель)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчера ресурсов Azure и классическом. Обязательно изучите [модели и инструменты развертывания](../azure-resource-manager/resource-manager-deployment-model.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure. Для просмотра документации hello для различных средств, выбрав параметр hello верхней части этой статьи. В этой статье рассматриваются hello классической модели развертывания.
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Образец Hello Azure PowerShell приведенную ниже команду ожидать простой среде уже создан на основании hello сценарии выше. Toorun hello команд, отображаемых в этом документе, создать среды hello, показанный на [Создание виртуальной сети (классические), с помощью PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Создать hello UDR для подсети hello переднего плана
Таблица маршрутов toocreate hello и маршрутов для подсети hello переднего плана, в зависимости от варианта hello выше, выполните следующие шаги hello.

1. Выполните следующие команды toocreate hello таблицы маршрутов для подсети интерфейса hello:

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. Запустите все toohello внутренней подсети (192.168.2.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Выполнения hello следующие таблицы маршрутов hello tooassociate команды с hello **переднего плана** подсети:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Создать hello UDR для hello внутренней подсети
Таблица маршрутов toocreate hello и маршрута, необходимые для повторного hello завершить подсети, в зависимости от варианта hello, выполните следующие шаги hello:

1. Выполните следующие команды toocreate hello таблицы маршрутов для подсети внутренней hello:

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. Запустите все toohello интерфейса подсети (192.168.1.0/24) toohello трафика, предназначенного hello, следующая команда toocreate маршрут в toosend таблицы маршрутов hello **FW1** виртуальной Машины (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Выполнения hello следующие таблицы маршрутов hello tooassociate команды с hello **серверной** подсети:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a>Включить IP-пересылки на приветствия FW1 виртуальной Машины

tooenable IP-пересылки в hello FW1 ВМ, полный hello, следующие шаги:

1. Выполните следующие команды toocheck hello состояние IP-пересылки hello.

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. Выполнения hello следующая команда tooenable IP-пересылки для hello *FW1* виртуальной Машины:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
