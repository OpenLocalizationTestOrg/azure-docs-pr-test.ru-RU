---
title: "aaaCreate виртуальной сети - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate в виртуальной сети с помощью PowerShell."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a>Создание виртуальной сети с помощью PowerShell

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую. Корпорация Майкрософт рекомендует создать ресурсы с помощью модели развертывания диспетчера ресурсов hello. Дополнительные сведения о toolearn hello различий между моделями hello двух чтения hello [модели развертывания Azure понять](../azure-resource-manager/resource-manager-deployment-model.md) статьи.
 
В этой статье объясняется, как toocreate виртуальной сети путем развертывания диспетчера ресурсов hello модели с помощью PowerShell. Также можно создать виртуальную сеть через диспетчер ресурсов с помощью других средств или создайте виртуальную сеть через hello классической модели развертывания, выбрав другой вариант hello после списка:

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

toocreate, виртуальной сети, с помощью PowerShell, полные hello следующие шаги:

1. Установка и настройка Azure PowerShell, выполнив указанные ниже действия hello в hello [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.

2. При необходимости создайте новую группу ресурсов, как показано ниже. В этом случае нужно создать группу ресурсов с именем *TestRG*. Дополнительные сведения о группах ресурсов см. в разделе "Группы ресурсов" [обзора Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    Ожидаемые выходные данные:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. Создайте новую виртуальную сеть с именем *TestVNet*.

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    Ожидаемые выходные данные:

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. Сохранить hello объекта виртуальной сети в переменной:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > Можно объединить шаги 3 и 4, выполнив команду `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.
   > 

5. Добавьте переменную подсети toohello новой виртуальной сети:

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    Ожидаемые выходные данные:
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. Повторите шаг 5 выше для каждой подсети требуется toocreate. Hello следующая команда создает hello *серверной* подсети для hello сценария:

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. Несмотря на то, что вы создаете подсетей, они в настоящее время только существуют в локальной переменной используется tooretrieve hello hello виртуальной сети, созданных на шаге 4 выше. hello изменения toosave tooAzure, запустите hello следующую команду:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    Ожидаемые выходные данные:
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как tooconnect:

- Виртуальная сеть виртуальной машины (VM) tooa, считывая hello [создания виртуальной Машины Windows](../virtual-machines/virtual-machines-windows-ps-create.md) статьи. Вместо создания виртуальной сети и подсети в шагах hello hello статей, можно выбрать существующей виртуальной сети и подсети tooconnect для виртуальной Машины.
- Здравствуйте, считывая hello виртуальных сетей в виртуальной сети tooother [подключение виртуальных сетей](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) статьи.
- tooan Hello виртуальной сети в локальной сети с помощью виртуальной частной сети сеть сеть (VPN) или канал ExpressRoute. Дополнительные сведения в разделе hello [подключения локальной сети tooan виртуальной сети с помощью VPN сайтами](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) и [связывание виртуальной сети tooan канал ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md) статей.
