---
title: "Настройка принудительного туннелирования для подключений типа \"сеть — сеть\" Azure (классическая модель) | Документация Майкрософт"
description: "Как tooredirect или «принудительно» все tooyour назад Интернета трафик локального расположения."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a>Настройка принудительного туннелирования с помощью hello классической модели развертывания

Принудительное туннелирование позволяет перенаправлять или «принудительно» все в локальное расположение задней tooyour Интернета трафик через туннель VPN сайт-сайт для проверки и аудита. Это критически важное требование безопасности, имеющееся в большинстве корпоративных ИТ-политик. Без принудительного туннелирования Интернет-трафик из виртуальных машин в Azure будет всегда проходить из сетевой инфраструктуры Azure непосредственно из toohello Интернета, без параметра tooallow hello вы tooinspect или аудита hello трафика. Несанкционированный доступ через Интернет потенциально может привести tooinformation раскрытию или другие виды угроз безопасности.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

В этой статье описывается настройка принудительного туннелирования для виртуальных сетей, созданных с помощью hello классической модели развертывания. Принудительное туннелирование можно настроить с помощью PowerShell, не через портал hello. Tooconfigure принудительного туннелирования для модели развертывания диспетчера ресурсов hello из hello, следуя раскрывающегося списка выберите классический статьи:

> [!div class="op_single_selector"]
> * [PowerShell — классическая модель](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell — Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a>Требования и рекомендации
В Azure принудительное туннелирование настраивается с помощью определяемых пользователем маршрутов виртуальной сети (UDR). Перенаправление трафика tooan из локального сайта выражается как шлюз Azure VPN toohello маршрут по умолчанию. Hello следующем разделе перечислены hello текущее ограничение таблицы маршрутизации hello и маршрутов для виртуальной сети Azure.

* Каждая подсеть виртуальной сети имеет встроенные системные таблицы маршрутизации. Таблица маршрутизации Hello система имеет следующие три группы маршрутов hello:

  * **Локальные маршруты виртуальной сети:** непосредственно toohello целевым ВМ в hello одной виртуальной сети.
  * **Локальные маршруты:** toohello VPN-шлюз Azure.
  * **Маршрут по умолчанию:** напрямую toohello Интернет. Пакеты, предназначенные toohello частных IP-адресов не соответствует ни hello предыдущие два маршруты, будут удалены.
* С выпуском hello определяемых пользователем маршрутов можно создать маршрутизации tooadd таблицы маршрут по умолчанию и затем связать hello маршрутизации таблицы tooyour виртуальной сети подсетями tooenable принудительного туннелирования в этих подсетях.
* Необходимо tooset «сайт по умолчанию» среди hello между организациями подключенных toohello локальных сайтов виртуальной сети.
* Принудительное туннелирование должно быть сопоставлено с виртуальной сетью, в которой есть VPN-шлюз с динамической маршрутизацией (а не статический шлюз).
* Принудительное туннелирование ExpressRoute не настраивается с помощью этого механизма, но вместо этого обеспечивается объявление маршрута по умолчанию через hello ExpressRoute BGP сеансы пиринга. См. в разделе hello [документации по ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) для получения дополнительной информации.

## <a name="configuration-overview"></a>Общие сведения о настройке
В следующем примере hello проводном hello интерфейсной подсети не является принудительным. Hello рабочих нагрузок в hello внешней подсети можно продолжить tooaccept и из Интернета hello отвечающего toocustomer запросов. Hello промежуточной и внутренней подсетях выполняется Принудительное туннелирование. Все исходящие подключения из этих двух подсетей toohello Интернет будет tooan принудительной или перенаправления обратно на локальный сайт через одну приветствия туннели S2S VPN.

Это позволяет вам toorestrict и инспектировать доступ к Интернету из виртуальных машин или облачных служб в Azure, продолжая tooenable необходимые службы многоуровневые архитектуры. Также можно применить принудительного туннелирования toohello все виртуальные сети, если отсутствуют рабочие нагрузки с выходом в Интернет в виртуальных сетях.

![Принудительное туннелирование](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a>Перед началом работы
Проверьте наличие следующих элементов перед началом процедуры настройки hello.

* Подписка Azure. Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).
* Настроенная виртуальная сеть. 
* Hello последняя версия командлетов Azure PowerShell hello. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello.

## <a name="configure-forced-tunneling"></a>Настройка принудительного туннелирования
Привет, после процедуры помогут задать Принудительное туннелирование для виртуальной сети. действия по настройке Hello соответствуют файла конфигурации сети toohello виртуальной сети.

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

В этом примере hello виртуальной сети «MultiTier-VNet» имеет три подсети: 'Переднего плана» и «Midtier», «Внутренний» подсетей с подключениями четыре перекрестные: «DefaultSiteHQ» и тремя ветвями. 

Hello действия будут hello «DefaultSiteHQ» hello соединение сайта по умолчанию для принудительного туннелирования и настройте hello Midtier и Backend подсети toouse принудительного туннелирования.

1. Создайте таблицу маршрутизации. Используйте следующий командлет toocreate hello таблицы маршрутизации.

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. Добавьте таблицу маршрутизации toohello маршрута по умолчанию. 

  Hello следующий пример добавляет по умолчанию маршрута toohello таблицу маршрутизации, созданную на шаге 1. Обратите внимание, что hello только поддерживаемый маршрут — hello префикс назначения «0.0.0.0/0» toohello следующего прыжка «VPNGateway».

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. Свяжите hello маршрутизации таблицы toohello подсети. 

  После создания таблицы маршрутизации и добавления маршрута, используйте следующий пример tooadd hello или свяжите маршрута таблицы hello tooa-подсеть виртуальной сети. пример Hello добавляет hello маршрута таблицу «MyRouteTable» toohello Midtier и серверной подсети виртуальной сети MultiTier-VNet.

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. Назначьте сайт по умолчанию для принудительного туннелирования. 

  В предыдущих шага hello hello демонстрационных скриптах командлетов hello таблицы маршрутизации, которая связывается tootwo таблицы маршрутов hello hello подсетей виртуальной сети. Hello осталось tooselect среди межсайтовых подключений hello hello виртуальной сети, что узел по умолчанию hello или туннель.

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a>Дополнительные командлеты PowerShell
### <a name="toodelete-a-route-table"></a>toodelete таблицы маршрутов

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a>toolist таблицы маршрутов

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a>toodelete маршрута из таблицы маршрутизации

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a>tooremove маршрута из подсети

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a>таблицы маршрутов hello toolist, связанной с подсетью

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a>tooremove сайт по умолчанию из шлюза виртуальной сети VPN

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```