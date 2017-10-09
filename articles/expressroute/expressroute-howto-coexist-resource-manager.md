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
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a>Настройка параллельных подключений ExpressRoute и "сайт-сайт"
> [!div class="op_single_selector"]
> * [PowerShell — Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell — классическая модель](expressroute-howto-coexist-classic.md)
> 
> 

Настройка параллельных подключений VPN типа "сеть — сеть" и ExpressRoute дает целый ряд преимуществ. Настройка VPN сайтами как путь безопасный переход на другой ресурс для ExressRoute или использовать toosites tooconnect VPN на сайт-сайт, не подключен через ExpressRoute. Оба сценария в этой статье мы рассмотрим действия tooconfigure hello. В этой статье относится модели развертывания диспетчера ресурсов toohello и использует PowerShell. Эта конфигурация не доступны в hello портал Azure.

> [!IMPORTANT]
> Каналы ExpressRoute должен быть предварительно настроен, прежде чем выполнять приведенные ниже инструкции hello. Убедитесь в том, чтобы были выполнены направляющие hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-arm.md) и [Настройка маршрутизации](expressroute-howto-routing-arm.md) перед продолжением работы.
> 
> 

## <a name="limits-and-limitations"></a>Квоты и ограничения
* **Транзитная маршрутизация не поддерживается.** Нельзя настроить маршрутизацию (через Azure) между локальной сетью, подключенной к VPN типа "сеть — сеть", и локальной сетью, подключенной к ExpressRoute.
* **Номера SKU класса "Базовый" для шлюза не поддерживаются.** Необходимо использовать основные SKU, отличного от шлюза для обоих hello [шлюз ExpressRoute](expressroute-about-virtual-network-gateways.md) и hello [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Поддерживается только VPN-шлюз на основе маршрутов.** Необходимо использовать [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md) на основе маршрутов.
* **Для VPN-шлюза необходимо настроить статический маршрут.** Если локальной сети — подключенных tooboth ExpressRoute и сеть-сеть VPN, должен иметь статический маршрут настроен в вашей локальной сети tooroute hello сеть-сеть VPN подключения toohello общедоступный Интернет.
* **Шлюз ExpressRoute должен быть настроен и связан tooa канала.** Необходимо сначала создать шлюз ExpressRoute hello и связать его tooa цепи, прежде чем добавлять hello сеть-сеть VPN-шлюз.

## <a name="configuration-designs"></a>Схемы конфигурации
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Настройка VPN типа "сеть-сеть" как пути отработки отказа для ExpressRoute
VPN-подключение типа "сеть-сеть" можно настроить как службу архивации для ExpressRoute. Это относится только toovirtual сетей связанного toohello Azure частным путем пиринга. Для служб, доступ к которым осуществляется через пиринг Azure Public или Microsoft, решения для отработки отказа на основе VPN не существует. Hello канал ExpressRoute всегда является основной ссылки hello. Поток данных проходит через путь через виртуальную Частную сеть для hello только в том случае, если происходит сбой hello канал ExpressRoute.

> [!NOTE]
> Пока канал ExpressRoute предпочтительнее через виртуальную Частную сеть для, когда обоих маршрутах являются одинаковыми hello, Azure будет использовать hello длинного префикса соответствия toochoose hello маршрута к назначения hello пакета.
> 
> 

![Существуют одновременно](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Настройка toosites через виртуальную Частную сеть для tooconnect, не подключен через ExpressRoute
Можно настроить сети, где некоторые узлы подключаются непосредственно tooAzure через сеть-сеть VPN, и некоторые узлы подключаются через ExpressRoute. 

![Существуют одновременно](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> Виртуальную сеть нельзя настроить как транзитный маршрутизатор.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>При выборе действия toouse hello
Существует два разных набора toochoose процедуры из. процедуры настройки Hello выбранного зависит от того, имеется ли существующей виртуальной сети, которые должны tooconnect в, или вы хотите toocreate новую виртуальную сеть.

* Я нет виртуальной сети и требуется toocreate один.
  
    Если у вас еще нет виртуальной сети, выполните эти шаги, чтобы создать ее с помощью модели развертывания Resource Manager, а также создать подключение ExpressRoute и VPN типа "сеть — сеть". tooconfigure виртуальной сети, следуйте указаниям hello [toocreate новую виртуальную сеть и существующих соединений](#new).
* У меня уже есть виртуальная сеть с моделью развертывания Resource Manager.
  
    Возможно, у вас уже имеется виртуальная сеть, а также подключения к VPN типа "сеть-сеть" или к ExpressRoute. Hello [tooconfigure существующих соединений для уже существующей виртуальной сети](#add) разделе описан процесс удаления шлюза hello и создания новых ExpressRoute "и" сеть-сеть VPN-подключений. При создании новых подключений hello, hello действия должны выполняться в определенном порядке. Не используйте инструкции hello в других статьях toocreate, шлюзы и подключения.
  
    В этой процедуре создания соединений, которые могут сосуществовать требует вы toodelete шлюз и настраиваете новых шлюзов. Вы получите время простоя для подключений между организациями во время удаления и повторного создания шлюза и подключения, но не потребуется toomigrate любой из виртуальных машин и служб tooa новой виртуальной сети. Виртуальные машины и службы будут иметь доступ toocommunicate out через hello балансировки нагрузки во время настройки шлюза, если они являются toodo настроенный таким образом.

## <a name="new"></a>toocreate новую виртуальную сеть и существующих соединений
В этой процедуре подробно рассматривается создание виртуальной сети, а также параллельных подключений ExpressRoute и "сеть — сеть".

1. Установите последнюю версию hello hello командлетов Azure PowerShell. Сведения об установке hello командлетов см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview). Возможно, несколько отличаются от что вы не знакомы с Hello командлеты, которые можно использовать для этой конфигурации. Указать командлеты hello toouse убедиться, что в этих инструкциях.
2. Войдите в учетную запись tooyour и настройка среды hello.

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. Создайте виртуальную сеть и подсеть шлюза. Дополнительные сведения о настройке виртуальной сети hello см. в разделе [конфигурации виртуальной сети Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).
   
   > [!IMPORTANT]
   > Hello подсеть шлюза должна быть /27 или короткое префикс (например, /26 или /25).
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
   
    Сохраните конфигурацию виртуальной сети hello.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw"></a>Создайте шлюз ExpressRoute. Дополнительные сведения о конфигурации шлюза hello ExpressRoute см. в разделе [шлюз ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Hello GatewaySKU должно быть *Стандартная*, *HighPerformance*, или *UltraPerformance*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. Свяжите канал ExpressRoute toohello шлюз ExpressRoute hello. После завершения этого шага hello между локальной сетью и Azure через ExpressRoute, подключение выполняется. Дополнительные сведения об операции связывания hello см. в разделе [tooExpressRoute связь виртуальных сетей](expressroute-howto-linkvnet-arm.md).

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a>Далее создайте VPN-шлюз типа "сеть — сеть". Дополнительные сведения о конфигурации шлюза VPN hello см. в разделе [настроить виртуальную сеть с подключением сайт-сайт](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md). Hello GatewaySKU должно быть *Стандартная*, *HighPerformance*, или *UltraPerformance*. Hello VpnType должен *routebased*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    Шлюз VPN Azure поддерживает протокол маршрутизации BGP. Можно указать ASN (номер AS) для этой виртуальной сети путем добавления коммутатора hello - Asn в hello следующую команду. Указание этого параметра не будет по умолчанию tooAS номер 65515.

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    Здравствуйте, BGP пиринг IP и hello как число, используемое для шлюза VPN hello в $azureVpn.BgpSettings.BgpPeeringAddress и $azureVpn.BgpSettings.Asn Azure можно найти. Дополнительные сведения см. в статье [Настройка BGP на VPN-шлюзах Azure с помощью Azure Resource Manager и PowerShell](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md).
7. Создайте сущность VPN-шлюза локального сайта. Эта команда не настраивает локальный VPN-шлюз. Вместо этого позволяет tooprovide hello локального шлюза параметры, такие как общедоступный IP-адрес hello и hello локального адресного пространства, hello VPN-шлюз Azure для подключения tooit.
   
    Если локальное устройство VPN поддерживает только статическую маршрутизацию, можно настроить статические маршруты hello в hello следующими способами:

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    Если локальное устройство VPN поддерживает hello BGP, и вы хотите tooenable динамической маршрутизации, необходимо tooknow hello BGP пиринг IP-адрес и hello как номер вашего локального VPN, который использует устройство.

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. Настройка локального устройства tooconnect toohello новые Azure VPN шлюза VPN. Дополнительные сведения о настройке VPN-устройства см. в статье [О VPN-устройствах для подключений VPN-шлюзов типа "сеть — сеть"](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
9. Шлюз через виртуальную Частную сеть для hello ссылку на Azure toohello локального шлюза.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a>tooconfigure существующих соединений для уже существующей виртуальной сети
При наличии существующей виртуальной сети, проверьте размер подсети шлюза hello. Если подсеть шлюза hello /28 или /29, необходимо сначала удалить шлюз виртуальной сети hello и увеличьте размер подсети шлюза hello. Hello действия, описанные в этом разделе показывается, как toodo.

Если подсеть шлюза hello /27 или больше и виртуальной сети hello подключен через ExpressRoute, можно пропустить шаги hello и продолжить слишком[«Шаг 6 — создать шлюз VPN сеть-сеть»](#vpngw) в предыдущем разделе hello. 

> [!NOTE]
> При удалении существующего шлюза hello ваших локальных машинах будут потеряны hello подключения tooyour виртуальной сети, при работе в этой конфигурации. 
> 
> 

1. Вам потребуется tooinstall hello последняя версия командлетов Azure PowerShell hello. Дополнительные сведения об установке командлетов см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview). Возможно, несколько отличаются от что вы не знакомы с Hello командлеты, которые можно использовать для этой конфигурации. Указать командлеты hello toouse убедиться, что в этих инструкциях. 
2. Удалите шлюз ExpressRoute или через виртуальную Частную сеть для существующих hello.

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. Удалите подсеть шлюза.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. Добавьте подсеть шлюза с префиксом /27 или больше.
   
   > [!NOTE]
   > При отсутствии недостаточно IP-адресов в вашей виртуальной сети шлюза hello tooincrease подсети размер tooadd необходимо больше пространства IP-адресов.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Сохраните конфигурацию виртуальной сети hello.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. На этом этапе у вас есть виртуальная сеть без шлюзов. toocreate новых шлюзов и завершения подключения, можно продолжить [шаг 4. Создайте шлюз ExpressRoute](#gw)в hello предшествующий набор шагов.

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a>tooadd точка сайт конфигурации toohello VPN-шлюза
Выполните действия hello ниже tooadd точки сайтами конфигурации tooyour VPN-шлюза в установке совместной работы.

1. Добавьте пул адресов VPN-клиента.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. Отправьте tooAzure hello VPN корневого сертификата для шлюза VPN. В этом примере предполагается, что корневой сертификат этого hello хранятся в hello локального компьютера, где выполняются следующие командлеты PowerShell hello.

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

Дополнительные сведения см. в статье [Настройка подключения типа "точка — сеть" к виртуальной сети с помощью PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).
