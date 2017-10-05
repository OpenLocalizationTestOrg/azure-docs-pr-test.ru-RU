---
title: "Настройка сосуществующих подключений VPN типа ExpressRoute и \"сеть — сеть\" с помощью модели Azure Resource Manager | Документация Майкрософт"
description: "В этой статье описывается настройка параллельных подключений ExpressRoute и VPN-подключений типа \"сеть — сеть\" для модели развертывания Resource Manager."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: b29147a37f9a90fc80e16b350ac9b91daac1d7f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a>Настройка параллельных подключений ExpressRoute и "сайт-сайт"
> [!div class="op_single_selector"]
> * [PowerShell — Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell — классическая модель](expressroute-howto-coexist-classic.md)
> 
> 

Настройка параллельных подключений VPN типа "сеть — сеть" и ExpressRoute дает целый ряд преимуществ. Вы можете настроить VPN типа "сеть — сеть" как защищенный путь отработки отказа для ExressRoute или использовать эту VPN для подключения к сайтам, не подключенным через ExpressRoute. В этой статье мы рассмотрим порядок действия в каждом из этих вариантов. Эта статья посвящена модели развертывания Resource Manager. Кроме того, в ней используется PowerShell. Эта конфигурация недоступна на портале Azure.

> [!IMPORTANT]
> Перед выполнением приведенных ниже инструкций необходимо настроить каналы ExpressRoute. Прежде чем продолжить, убедитесь, что выполнили все инструкции по [созданию канала ExpressRoute](expressroute-howto-circuit-arm.md) и [настройке маршрутизации](expressroute-howto-routing-arm.md).
> 
> 

## <a name="limits-and-limitations"></a>Квоты и ограничения
* **Транзитная маршрутизация не поддерживается.** Нельзя настроить маршрутизацию (через Azure) между локальной сетью, подключенной к VPN типа "сеть — сеть", и локальной сетью, подключенной к ExpressRoute.
* **Номера SKU класса "Базовый" для шлюза не поддерживаются.** Используйте для [ExpressRoute](expressroute-about-virtual-network-gateways.md) и [VPN-шлюза](../vpn-gateway/vpn-gateway-about-vpngateways.md) номера SKU другого класса.
* **Поддерживается только VPN-шлюз на основе маршрутов.** Необходимо использовать [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md) на основе маршрутов.
* **Для VPN-шлюза необходимо настроить статический маршрут.** Если локальная сеть подключена и к ExpressRoute, и к VPN типа "сеть — сеть", необходимо использовать статический маршрут, настроенный в локальной сети для маршрутизации VPN-подключения типа "сеть — сеть" к Интернету.
* **Сначала шлюз ExpressRoute нужно настроить, а затем связать с каналом.** Сначала нужно создать шлюз ExpressRoute, связать его с каналом, а затем добавить шлюз VPN типа "сеть — сеть".

## <a name="configuration-designs"></a>Схемы конфигурации
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Настройка VPN типа "сеть-сеть" как пути отработки отказа для ExpressRoute
VPN-подключение типа "сеть-сеть" можно настроить как службу архивации для ExpressRoute. Это относится только к виртуальным сетям, привязанным к пути пиринга Azure Private. Для служб, доступ к которым осуществляется через пиринг Azure Public или Microsoft, решения для отработки отказа на основе VPN не существует. Канал ExpressRoute всегда является основной ссылкой. Данные передаются по пути VPN типа "сеть — сеть", только если канал ExpressRoute не справляется с этой задачей.

> [!NOTE]
> Хотя канал ExpressRoute лучше использовать для VPN типа "сеть — сеть", когда оба маршрута одинаковы, Azure будет выбирать маршрут для назначения пакета по совпадению самого длинного префикса.
> 
> 

![Существуют одновременно](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a>Настройка VPN типа "сеть-сеть" для подключения к сайтам, не подключенным через ExpressRoute
Сети можно настроить таким образом, чтобы одни из них подключались непосредственно к Azure по VPN типа "сеть-сеть", а другие — через ExpressRoute. 

![Существуют одновременно](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> Виртуальную сеть нельзя настроить как транзитный маршрутизатор.
> 
> 

## <a name="selecting-the-steps-to-use"></a>Выбор действий для использования
Существует два типа процедур. Выбор процедуры настройки зависит от того, существует ли уже виртуальная сеть, к которой необходимо подключиться, или требуется создать ее.

* У меня нет виртуальной сети, и мне нужно ее создать.
  
    Если у вас еще нет виртуальной сети, выполните эти шаги, чтобы создать ее с помощью модели развертывания Resource Manager, а также создать подключение ExpressRoute и VPN типа "сеть — сеть". Чтобы настроить виртуальную сеть, выполните шаги, описанные в разделе [Создание виртуальной сети и параллельных подключений](#new).
* У меня уже есть виртуальная сеть с моделью развертывания Resource Manager.
  
    Возможно, у вас уже имеется виртуальная сеть, а также подключения к VPN типа "сеть-сеть" или к ExpressRoute. В разделе [Настройка параллельных подключений для существующей виртуальной сети](#add) представлены пошаговые инструкции по удалению шлюза и созданию подключений ExpressRoute и VPN типа "сеть — сеть". Все шаги по созданию параллельных подключений необходимо выполнять в определенном порядке. При создании шлюзов и подключений не пользуйтесь инструкциями, взятыми из других статей.
  
    Чтобы создать параллельные подключения по этой процедуре, необходимо удалить существующий шлюз и настроить новые. Подключение между организациями прервется на время удаления и повторного создания шлюза и подключений, но вам не потребуется выполнять миграцию всех виртуальных машин и служб в новую виртуальную сеть. Виртуальные машины и службы смогут по-прежнему осуществлять связь через балансировщик нагрузки во время настройки шлюза, если они настроены соответствующим образом.

## <a name="new"></a>Создание новой виртуальной сети и параллельных подключений
В этой процедуре подробно рассматривается создание виртуальной сети, а также параллельных подключений ExpressRoute и "сеть — сеть".

1. Установите последнюю версию командлетов Azure PowerShell. Дополнительные сведения об установке командлетов см. в статье об [установке и настройке Azure PowerShell](/powershell/azure/overview). Командлеты, которые будут использоваться для этой конфигурации, могут немного отличаться от уже знакомых вам. Обязательно используйте командлеты, указанные в инструкциях.
2. Войдите в учетную запись и настройте среду.

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. Создайте виртуальную сеть и подсеть шлюза. Дополнительные сведения о настройке виртуальной сети см. в статье [Создание виртуальной сети с помощью PowerShell](../virtual-network/virtual-networks-create-vnet-arm-ps.md).
   
   > [!IMPORTANT]
   > Подсеть шлюза должна иметь префикс /27 или более короткий префикс (например, /26 или /25).
   > 
   > 
   
    Создайте виртуальную сеть.

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    Добавьте подсети.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Сохраните конфигурацию виртуальной сети.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw"></a>Создайте шлюз ExpressRoute. Дополнительные сведения о настройке шлюза ExpressRoute см. в статье [Настройка шлюза виртуальной сети для ExpressRoute с помощью диспетчера ресурсов и PowerShell](expressroute-howto-add-gateway-resource-manager.md). Параметр GatewaySKU должен иметь значение *Standard*, *HighPerformance* или *UltraPerformance*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. Свяжите шлюз ExpressRoute с каналом ExpressRoute. После выполнения этого действия подключение локальной сети к Azure через ExpressRoute будет установлено. Дополнительные сведения об операции связывания см. в статье [Связывание виртуальной сети с каналом ExpressRoute](expressroute-howto-linkvnet-arm.md).

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a>Далее создайте VPN-шлюз типа "сеть — сеть". Дополнительные сведения о настройке VPN-шлюза см. в статье [Создание виртуальной сети с подключением типа "сеть — сеть" с помощью PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md). Параметр GatewaySKU должен иметь значение *Standard*, *HighPerformance* или *UltraPerformance*. Параметр VpnType должен иметь значение *RouteBased*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    Шлюз VPN Azure поддерживает протокол маршрутизации BGP. Для этой виртуальной сети можно указать ASN (номер AS), добавив параметр -Asn в команду ниже. Без этого параметра номер AS получит значение по умолчанию — 65515.

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    IP-адрес пиринга BGP и номер AS, используемый Azure для VPN-шлюза, можно найти в атрибутах $azureVpn.BgpSettings.BgpPeeringAddress и $azureVpn.BgpSettings.Asn. Дополнительные сведения см. в статье [Настройка BGP на VPN-шлюзах Azure с помощью Azure Resource Manager и PowerShell](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md).
7. Создайте сущность VPN-шлюза локального сайта. Эта команда не настраивает локальный VPN-шлюз. Она только позволяет указать параметры локального шлюза, такие как общедоступный IP-адрес и локальное адресное пространство, чтобы VPN-шлюз Azure мог подключиться к нему.
   
    Если локальное VPN-устройство поддерживает только статическую маршрутизацию, статические маршруты можно настроить следующим образом:

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    Если локальное VPN-устройство поддерживает протокол BGP, чтобы включить динамическую маршрутизацию, необходимо знать используемый этим устройством IP-адрес пиринга BGP и номер AS.

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for the BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. Настройте локальное VPN-устройство для подключения к новому VPN-шлюзу Azure. Дополнительные сведения о настройке VPN-устройства см. в статье [О VPN-устройствах для подключений VPN-шлюзов типа "сеть — сеть"](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
9. Свяжите VPN-шлюз к сети типа "сеть-сеть" в Azure с локальным шлюзом.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a>Настройка параллельных подключений для существующей виртуальной сети
При наличии существующей виртуальной сети проверьте размер подсети шлюза. Если размер подсети шлюза — /28 или /29, необходимо сначала удалить шлюз виртуальной сети и увеличить размер подсети шлюза. В этом разделе показано, как это сделать.

Если размер подсети шлюза — /27 или больше, а виртуальная сеть подключается с помощью ExpressRoute, можно пропустить описанные ниже шаги и перейти к шагу 6 ( [Создание VPN-шлюза подключения типа "сеть — сеть"](#vpngw) ) в предыдущем разделе. 

> [!NOTE]
> При удалении существующего шлюза локальные пользователи потеряют подключение к виртуальной сети на время выполнения этой настройки. 
> 
> 

1. Вам потребуется установить последнюю версию командлетов Azure PowerShell. Дополнительные сведения об установке командлетов см. в статье об [установке и настройке Azure PowerShell](/powershell/azure/overview). Командлеты, которые будут использоваться для этой конфигурации, могут немного отличаться от уже знакомых вам. Обязательно используйте командлеты, указанные в инструкциях. 
2. Удалите для сети типа "сеть — сеть" существующий VPN-шлюз или шлюз ExpressRoute.

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. Удалите подсеть шлюза.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. Добавьте подсеть шлюза с префиксом /27 или больше.
   
   > [!NOTE]
   > Если в виртуальной сети недостаточно свободных IP-адресов для увеличения размера подсети шлюза, необходимо добавить дополнительные пространства IP-адресов.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Сохраните конфигурацию виртуальной сети.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. На этом этапе у вас есть виртуальная сеть без шлюзов. Чтобы создать новые шлюзы и завершить подключение, перейдите к шагу 4 ( [Создайте шлюз ExpressRoute](#gw)) из предыдущего раздела.

## <a name="to-add-point-to-site-configuration-to-the-vpn-gateway"></a>Добавление конфигурации "точка — сеть" к VPN-шлюзу
Чтобы добавить конфигурацию "точка — сеть" к VPN-шлюзу при настройке параллельных подключений, выполните следующее.

1. Добавьте пул адресов VPN-клиента.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. Отправьте корневой сертификат VPN в Azure для VPN-шлюза. В этом примере подразумевается, что корневой сертификат хранится на локальном компьютере, где выполняются следующие командлеты PowerShell.

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

Дополнительные сведения см. в статье [Настройка подключения типа "точка — сеть" к виртуальной сети с помощью PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об ExpressRoute см. в статье [Вопросы и ответы по ExpressRoute](expressroute-faqs.md).
