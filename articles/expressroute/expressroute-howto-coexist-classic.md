---
title: "Настройка сосуществующих подключений VPN типа ExpressRoute и \"сеть — сеть\" с помощью классической модели Azure | Документация Майкрософт"
description: "В этой статье описывается настройка ExpressRoute и через виртуальную Частную сеть для подключения, могут сосуществовать для hello классической модели развертывания."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a>Настройка параллельных подключений ExpressRoute и "сайт — сайт" (классическая версия)
> [!div class="op_single_selector"]
> * [PowerShell — Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell — классическая модель](expressroute-howto-coexist-classic.md)
> 
> 

Наличие возможности hello tooconfigure через виртуальную Частную сеть для и ExpressRoute имеет несколько преимуществ. Можно настроить через виртуальную Частную сеть — как путь безопасный переход на другой ресурс для ExressRoute или использовать toosites tooconnect VPN на сайт-сайт, не подключен через ExpressRoute. Hello tooconfigure действия будут рассмотрены оба сценария в этой статье. Эта статья относится toohello классической модели развертывания. Эта конфигурация не доступна на портале hello.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**О моделях развертывания Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> Каналы ExpressRoute должен быть предварительно настроен, прежде чем выполнять приведенные ниже инструкции hello. Убедитесь в том, чтобы были выполнены направляющие hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-classic.md) и [Настройка маршрутизации](expressroute-howto-routing-classic.md) перед выполнением приведенных ниже шагов hello.
> 
> 

## <a name="limits-and-limitations"></a>Квоты и ограничения
* **Транзитная маршрутизация не поддерживается.** Нельзя настроить маршрутизацию (через Azure) между локальной сетью, подключенной к VPN типа "сеть — сеть", и локальной сетью, подключенной к ExpressRoute.
* **Соединение типа "точка — сеть" не поддерживается.** Не удается включить toohello подключений VPN точки сайтами одной виртуальной сети, подключенной tooExpressRoute. Точка сеть VPN и ExpressRoute не может использоваться совместно для hello же виртуальной сети.
* **Принудительное туннелирование нельзя включить hello через виртуальную Частную сеть для шлюза.** Можно только «принудительно» все Интернета трафика задней tooyour локальной сети с помощью ExpressRoute.
* **Номера SKU класса "Базовый" для шлюза не поддерживаются.** Необходимо использовать основные SKU, отличного от шлюза для обоих hello [шлюз ExpressRoute](expressroute-about-virtual-network-gateways.md) и hello [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Поддерживается только VPN-шлюз на основе маршрутов.** Необходимо использовать [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md) на основе маршрутов.
* **Для VPN-шлюза необходимо настроить статический маршрут.** Если локальной сети — подключенных tooboth ExpressRoute и сеть-сеть VPN, должен иметь статический маршрут настроен в вашей локальной сети tooroute hello сеть-сеть VPN подключения toohello общедоступный Интернет.
* **Шлюз ExpressRoute необходимо настроить в первую очередь.** Сначала необходимо создать шлюз ExpressRoute hello, перед добавлением hello через виртуальную Частную сеть для шлюза.

## <a name="configuration-designs"></a>Схемы конфигурации
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Настройка VPN типа "сеть-сеть" как пути отработки отказа для ExpressRoute
VPN-подключение типа "сеть-сеть" можно настроить как службу архивации для ExpressRoute. Это относится только toovirtual сетей связанного toohello Azure частным путем пиринга. Для служб, доступ к которым осуществляется через пиринг Azure Public или Microsoft, решения для отработки отказа на основе VPN не существует. Hello канал ExpressRoute всегда является основной ссылки hello. Только в том случае, если происходит сбой hello канал ExpressRoute через hello через виртуальную Частную сеть для пути будет потока данных. 

> [!NOTE]
> Пока канал ExpressRoute предпочтительнее через виртуальную Частную сеть для, когда обоих маршрутах являются одинаковыми hello, Azure будет использовать hello длинного префикса соответствия toochoose hello маршрута к назначения hello пакета.
> 
> 

![Существуют одновременно](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Настройка toosites через виртуальную Частную сеть для tooconnect, не подключен через ExpressRoute
Можно настроить сети, где некоторые узлы подключаются непосредственно tooAzure через сеть-сеть VPN, и некоторые узлы подключаются через ExpressRoute. 

![Существуют одновременно](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> Настроить виртуальную сеть как транзитный маршрутизатор нельзя.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>При выборе действия toouse hello
Существует два разных набора toochoose процедуры из заказа tooconfigure подключений, которые могут сосуществовать. процедуры настройки Hello выбранного будет зависеть от наличия у существующей виртуальной сети, которые должны tooconnect в, или вы хотите toocreate новую виртуальную сеть.

* Я нет виртуальной сети и требуется toocreate один.
  
    Если у вас еще нет виртуальной сети, эта процедура поможет создать новую виртуальную сеть с помощью hello классической модели развертывания и создание новых ExpressRoute "и" сеть-сеть VPN-подключений. tooconfigure hello приведенным ниже инструкциям в разделе статьи hello [toocreate новую виртуальную сеть и существующих соединений](#new).
* У меня уже есть виртуальная сеть с классической моделью развертывания.
  
    Возможно, у вас уже имеется виртуальная сеть, а также подключения к VPN типа "сеть-сеть" или к ExpressRoute. Здравствуйте раздела статьи [tooconfigure coexsiting соединений для уже существующей виртуальной сети](#add) поможет выполнить удаление шлюза hello и затем создавать новые ExpressRoute и через виртуальную Частную сеть для подключения. Обратите внимание, что при создании новых подключений hello, hello действия должны выполняться очень определенным образом. Не используйте инструкции hello в других статьях toocreate, шлюзы и подключения.
  
    В этой процедуре создания соединений, которые могут сосуществовать потребуется вы toodelete шлюз и затем настройте новых шлюзов. Это означает, что имеется время простоя для подключений между организациями во время удаления и повторного создания шлюза и подключения, но не потребуется toomigrate любой из виртуальных машин и служб tooa новой виртуальной сети. Виртуальные машины и службы будут иметь доступ toocommunicate out через hello балансировки нагрузки во время настройки шлюза, если они являются toodo настроенный таким образом.

## <a name="new"></a>toocreate новую виртуальную сеть и существующих соединений
В этой процедуре подробно рассматривается создание виртуальной сети, а также параллельных подключений ExpressRoute и "сеть-сеть".

1. Вам потребуется tooinstall hello последняя версия командлетов Azure PowerShell hello. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello. Обратите внимание, что командлеты hello, который будет использоваться для этой конфигурации может быть немного отличается от что вы не знакомы с. Указать командлеты hello toouse убедиться, что в этих инструкциях. 
2. Создайте схему для виртуальной сети. Дополнительные сведения о схеме конфигурации hello см. в разделе [схема конфигурации виртуальной сети Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   
    При создании схемы, убедитесь, что используется hello следующие значения:
   
   * Hello подсеть шлюза для виртуальной сети hello должно быть /27 или короткое префикс (например, /26 или /25).
   * Тип подключения шлюза Hello» выделенные».
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. После создания и настройки файла схемы xml, отправьте файл hello. Это будет созданием виртуальной сети.
   
    Используйте следующий командлет tooupload hello файл, заменив значение hello свои собственные.
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <a name="gw"></a>Создайте шлюз ExpressRoute. Быть toospecify убедиться, что hello GatewaySKU как *стандартные*, *HighPerformance*, или *UltraPerformance* и hello тип шлюза как *DynamicRouting*.
   
    Здравствуйте, используйте следующий образец, подставив собственные значения hello.
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. Свяжите канал ExpressRoute toohello шлюз ExpressRoute hello. После завершения этого шага hello между локальной сетью и Azure через ExpressRoute, подключение выполняется.
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <a name="vpngw"></a>Далее создайте VPN-шлюз типа "сеть — сеть". Hello GatewaySKU должно быть *Стандартная*, *HighPerformance*, или *UltraPerformance* и hello тип шлюза должен быть *DynamicRouting*.
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    tooretrieve hello виртуальной сети шлюза параметров, включая идентификатор шлюза hello и hello открытый IP-адрес использовать hello `Get-AzureVirtualNetworkGateway` командлета.
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. Создайте сущность VPN-шлюза локального сайта. Эта команда не настраивает локальный VPN-шлюз. Вместо этого позволяет tooprovide hello локального шлюза параметры, такие как общедоступный IP-адрес hello и hello локального адресного пространства, hello VPN-шлюз Azure для подключения tooit.
   
   > [!IMPORTANT]
   > локальном сайте hello через виртуальную Частную сеть для Hello не определен в hello netcfg. Вместо этого необходимо использовать это параметры командлета toospecify hello локального сайта. Нельзя определить с помощью портала или файла netcfg hello.
   > 
   > 
   
    Следующий пример, заменив значения hello собственные используйте hello.
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > Если локальная сеть имеет несколько маршрутов, их все можно передать как массив.  $MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")  
   > 
   > 

    tooretrieve hello виртуальной сети шлюза параметров, включая идентификатор шлюза hello и hello открытый IP-адрес использовать hello `Get-AzureVirtualNetworkGateway` командлета. См. следующий пример hello.

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. Настройка локального устройства tooconnect toohello нового шлюза VPN. Используйте сведения hello, полученный на шаге 6, при настройке VPN-устройства. Дополнительные сведения о настройке VPN-устройства см. в статье [О VPN-устройствах для подключений VPN-шлюзов типа "сеть — сеть"](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
2. Шлюз через виртуальную Частную сеть для hello ссылку на Azure toohello локального шлюза.
   
    В этом примере connectedEntityId — идентификатор hello локального шлюза, который можно получить, выполнив `Get-AzureLocalNetworkGateway`. VirtualNetworkGatewayId можно найти с помощью hello `Get-AzureVirtualNetworkGateway` командлета. После выполнения этого шага hello между локальной сетью и Azure через hello подключение через виртуальную Частную сеть для подключения.

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <a name="add"></a>tooconfigure coexsiting соединений для уже существующей виртуальной сети
При наличии существующей виртуальной сети, проверьте размер подсети шлюза hello. Если подсеть шлюза hello /28 или /29, необходимо сначала удалить шлюз виртуальной сети hello и увеличьте размер подсети шлюза hello. Hello действия, описанные в этом разделе будет показано, как toodo.

Если подсеть шлюза hello /27 или больше и виртуальной сети hello подключен через ExpressRoute, можно пропустить шаги hello и продолжить слишком[«Шаг 6 — создать шлюз VPN сеть-сеть»](#vpngw) в предыдущем разделе hello.

> [!NOTE]
> При удалении существующего шлюза hello ваших локальных машинах будут потеряны hello подключения tooyour виртуальной сети, при работе в этой конфигурации.
> 
> 

1. Вам потребуется tooinstall hello последнюю версию hello командлеты PowerShell диспетчера ресурсов Azure. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello. Обратите внимание, что командлеты hello, который будет использоваться для этой конфигурации может быть немного отличается от что вы не знакомы с. Указать командлеты hello toouse убедиться, что в этих инструкциях. 
2. Удалите шлюз ExpressRoute или через виртуальную Частную сеть для существующих hello. Используйте hello следующий командлет, заменив значения hello собственные.
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. Экспорт схемы hello виртуальной сети. Используйте hello следующий командлет PowerShell, заменив значения hello собственные.
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. Схема файла конфигурации сети hello следует измените, чтобы подсеть шлюза hello /27 или короткое префикс (например, /26 или /25). См. следующий пример hello. 
   
   > [!NOTE]
   > При отсутствии недостаточно IP-адресов в вашей виртуальной сети шлюза hello tooincrease подсети размер tooadd необходимо больше пространства IP-адресов. Дополнительные сведения о схеме конфигурации hello см. в разделе [схема конфигурации виртуальной сети Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. Если предыдущие шлюза VPN сайт-сайт, необходимо также изменить тип подключения hello слишком**Dedicated**.
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. На этом этапе вы будете иметь виртуальную сеть без шлюзов. toocreate новых шлюзов и завершения подключения, можно продолжить [шаг 4. Создайте шлюз ExpressRoute](#gw)в hello предшествующий набор шагов.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md)

