---
title: "Настройка принудительного туннелирования для подключений типа \"сеть — сеть\" с помощью Resource Manager | Документация Майкрософт"
description: "Как tooredirect или «принудительно» все tooyour назад Интернета трафик локального расположения."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a>Настройка принудительного туннелирования с помощью модели развертывания диспетчера ресурсов Azure hello

Принудительное туннелирование позволяет перенаправлять или «принудительно» все в локальное расположение задней tooyour Интернета трафик через туннель VPN сайт-сайт для проверки и аудита. Это критически важное требование безопасности, имеющееся в большинстве корпоративных ИТ-политик. Без принудительного туннелирования Интернет-трафик из виртуальных машин в Azure всегда проходит через из сетевой инфраструктуры Azure непосредственно из toohello Интернета, без параметра tooallow hello вы tooinspect или аудита hello трафика. Несанкционированный доступ через Интернет потенциально может привести tooinformation раскрытию или другие виды угроз безопасности.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

В этой статье описывается настройка принудительного туннелирования для виртуальных сетей, созданные с помощью модели развертывания диспетчера ресурсов hello. Принудительное туннелирование можно настроить с помощью PowerShell, не через портал hello. Tooconfigure принудительного туннелирования для hello классической модели развертывания из hello, следуя раскрывающегося списка выберите классический статьи:

> [!div class="op_single_selector"]
> * [PowerShell — классическая модель](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell — Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a>Сведения о принудительном туннелировании

Hello, следующая диаграмма иллюстрирует, как работает Принудительное туннелирование. 

![Принудительное туннелирование](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

В приведенном выше примере hello hello проводном подсети не является принудительным переднего плана. Hello рабочих нагрузок в hello внешней подсети можно продолжить tooaccept и из Интернета hello отвечающего toocustomer запросов. Hello промежуточной и внутренней подсетях выполняется Принудительное туннелирование. Все исходящие подключения из этих двух подсетей toohello Интернет будет tooan принудительной или перенаправления обратно на локальный сайт через одну приветствия туннели S2S VPN.

Это позволяет вам toorestrict и инспектировать доступ к Интернету из виртуальных машин или облачных служб в Azure, продолжая tooenable необходимые службы многоуровневые архитектуры. Если в виртуальных сетях не рабочих нагрузок с выходом в Интернет, также можно применить принудительного туннелирования toohello всех виртуальных сетях.

## <a name="requirements-and-considerations"></a>Требования и рекомендации

В Azure принудительное туннелирование настраивается с помощью определяемых пользователем маршрутов виртуальной сети. Перенаправление трафика tooan из локального сайта выражается как шлюз Azure VPN toohello маршрут по умолчанию. Сведения об определяемых пользователем маршрутах см. в статье [Определяемые пользователем маршруты и IP-пересылка](../virtual-network/virtual-networks-udr-overview.md).

* Каждая подсеть виртуальной сети имеет встроенные системные таблицы маршрутизации. Таблица маршрутизации Hello система имеет следующие три группы маршрутов hello:
  
  * **Локальные маршруты виртуальной сети:** непосредственно toohello целевым ВМ в hello одной виртуальной сети.
  * **Локальные маршруты:** toohello VPN-шлюз Azure.
  * **Маршрут по умолчанию:** напрямую toohello Интернет. Пакеты, предназначенные toohello частных IP-адресов не соответствует ни hello предыдущие два маршруты будут удалены.
* Эта процедура использует определяемых пользователем маршрутов (UDR) toocreate маршрутизации tooadd таблицы маршрут по умолчанию, а затем задать hello маршрутизации таблицы tooyour виртуальной сети подсетями tooenable принудительного туннелирования в этих подсетях.
* Принудительное туннелирование должно быть связано с виртуальной сетью, в которой есть VPN-шлюз на основе маршрута. Необходимо tooset «сайт по умолчанию» среди hello между организациями подключенных toohello локальных сайтов виртуальной сети. Кроме того hello из локального VPN-устройство должен быть настроен с помощью 0.0.0.0/0 как трафика селекторов. 
* Принудительное туннелирование ExpressRoute не настраивается с помощью этого механизма, но вместо этого обеспечивается объявление маршрута по умолчанию через hello ExpressRoute BGP сеансы пиринга. Дополнительные сведения см. в разделе hello [документации по ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="configuration-overview"></a>Общие сведения о настройке

Hello следующая процедура поможет создать группу ресурсов и виртуальной сети. Затем вы создадите VPN-шлюз и настроите принудительное туннелирование. В этой процедуре hello виртуальной сети «MultiTier-VNet» имеет три подсети: 'Переднего плана», «Midtier» и «Серверная часть» с четырьмя соединениях между организациями: «DefaultSiteHQ» и тремя ветвями.

шаги процедуры Hello задать hello «DefaultSiteHQ» hello подключения сайта по умолчанию для принудительного туннелирования, и настройке hello «Midtier» и «Серверная часть» подсетей toouse принудительного туннелирования.

## <a name="before-you-begin"></a>Перед началом работы

Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello.

### <a name="toolog-in"></a>toolog в

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a>Настройка принудительного туннелирования

1. Создайте группу ресурсов.

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. Создайте виртуальную сеть и укажите подсети.

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. Создайте hello шлюзы локальной сети.

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. Создайте правило, таблицы и маршрут маршрута hello.

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. Свяжите toohello таблицы маршрутов hello Midtier и подсетей серверной части.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Создайте hello шлюза с узлом по умолчанию. Это требует toocomplete некоторое время, иногда 45 минут или более, так как в создании и настройке шлюза hello.<br> Hello **- GatewayDefaultSite** hello параметр командлета, который позволяет hello принудительно маршрутизации toowork конфигурации, поэтому можете следить за tooconfigure этот параметр должным образом. Он доступен только в PowerShell 1.0 или более поздней версии.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. Установите hello сеть-сеть VPN-подключений.

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```