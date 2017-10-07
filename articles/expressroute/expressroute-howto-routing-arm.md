---
title: "Как tooconfigure маршрутизации (пиринг) для канала ExpressRoute: диспетчера ресурсов: PowerShell: Azure | Документы Microsoft"
description: "В этой статье содержится описание этапов hello для создания и подготовки hello private, public и Microsoft пиринг канал ExpressRoute. В этой статье также рассказывается, как состояние toocheck hello, обновления или удаления пиринги для своего канала."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a>Создание и изменение пиринга для канала ExpressRoute с помощью PowerShell

Эта статья поможет вам создавать и управлять ими конфигурации маршрутизации для канала ExpressRoute в модели развертывания диспетчера ресурсов hello, с помощью PowerShell. Можно также проверить состояние hello, update или delete и отзыв пиринги за канал ExpressRoute. Если вы хотите toouse toowork другой метод с ваш канал, выберите статью из hello после списка:

> [!div class="op_single_selector"]
> * [Портал Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Интерфейс командной строки Azure](howto-routing-cli.md)
> * [Видео — частный пиринг](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Видео — общедоступный пиринг](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Видео — пиринг Майкрософт](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (классическая модель)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Предварительные требования для настройки

* Вам потребуется hello последнюю версию hello командлеты PowerShell диспетчера ресурсов Azure. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview). 
* Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md) страницы hello [требования к маршрутизации](expressroute-routing.md) страницы и hello [рабочих процессов](expressroute-workflows.md) страницы перед началом настройки.
* Вам потребуется активный канал ExpressRoute. Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-arm.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить. Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен для вас командлеты hello может toorun toobe в этой статье.

Эти инструкции применяются только toocircuits, созданных с помощью предложения службы связи уровня 2 поставщиков услуг. Если ваш поставщик услуг подключения предлагает услуги третьего уровня (обычно это IPVPN, например MPLS), то он возьмет на себя настройку маршрутизации и управление ею.

> [!IMPORTANT]
> Мы сейчас не объявляет пиринги настроен поставщиками услуг через портал управления службами hello. Такая возможность будет предоставлена позже. Перед настройкой пирингов BGP уточните информацию у поставщика услуг.
> 
> 

Для каждого канала ExpressRoute можно настроить один, два или три пиринга (частный пиринг Azure, общедоступный пиринг Azure и пиринг Microsoft). Пиринги можно настраивать в любом порядке, Тем не менее необходимо выполнить настройку hello из каждого из них пиринга одновременно. 

## <a name="azure-private-peering"></a>Частный пиринг Azure

Этот раздел поможет вам создать, получить, обновление и удаление hello Azure закрытая конфигурация пиринга канал ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate открытого пиринга Azure

1. Импортируйте модуль PowerShell hello для ExpressRoute.

  Необходимо установить установщик последнюю PowerShell hello из [коллекции PowerShell](http://www.powershellgallery.com/) и импортируйте модули диспетчера ресурсов Azure hello в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello. Вам потребуется toorun PowerShell с правами администратора.

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  Импортируйте все модули AzureRM.* hello внутри hello известный диапазон версию семантики.

  ```powershell
  Import-AzureRM
  ```

  Можно импортировать также просто выберите модуль внутри hello известный диапазон версию семантики.

  ```powershell
  Import-Module AzureRM.Network 
  ```

  Войдите в учетную запись tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Выберите подписку hello требуется toocreate канал ExpressRoute.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Создайте канал ExpressRoute.

  Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-arm.md) и их подготовки с помощью поставщика услуг подключения hello.

  Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас. В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello. Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.
3. Убедитесь, что подготовлены, а также включить toomake цепь ExpressRoute hello. Используйте следующий пример hello.

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  Hello ответ — аналогично toohello в следующем примере:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Настройка открытого пиринга Azure для hello схемы. Убедитесь, что hello следующих элементов, прежде чем продолжить hello следующие шаги:

  * / 30 подсеть для основной ссылки hello. подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.
  * / 30 подсеть для дополнительной ссылки hello. подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.
  * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
  * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS. Для этого пиринга можно использовать частный номер AS. Не используйте номер 65515.
  * **Необязательно —** хэш MD5 при выборе toouse один.

  Используйте следующий пример tooconfigure Azure закрытого пиринга для своего канала hello.

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  При выборе toouse хэш MD5, используйте следующий пример hello:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.
  > 
  >

### <a name="tooview-azure-private-peering-details"></a>tooview Azure закрытого пиринга подробные сведения

Сведения о конфигурации можно получить с помощью hello в следующем примере:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate конфигурации закрытого пиринга Azure

Вы можете обновить любая часть конфигурации hello, используя следующий пример hello. В этом примере выполняется обновление hello VLAN ID канала hello из 100 too500.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a>toodelete открытого пиринга Azure

Пиринг конфигурации можно удалить, выполнив следующий пример hello.

> [!WARNING]
> Необходимо убедиться, что все виртуальные сети будут отключены от hello канал ExpressRoute перед запуском этого примера. 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a>Общедоступный пиринг Azure

Этот раздел поможет вам создать, получить, обновление и удаление hello Azure открытая конфигурация пиринга канал ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate частного пиринга Azure

1. Импортируйте модуль PowerShell hello для ExpressRoute.

  Необходимо установить установщик последнюю PowerShell hello из [коллекции PowerShell](http://www.powershellgallery.com/) и импортируйте модули диспетчера ресурсов Azure hello в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello. Вам потребуется toorun PowerShell с правами администратора.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  Импортируйте все модули AzureRM.* hello внутри hello известный диапазон версию семантики.

  ```powershell
  Import-AzureRM
  ```

  Можно импортировать также просто выберите модуль внутри hello известный диапазон версию семантики.

  ```powershell
  Import-Module AzureRM.Network
```

  Войдите в учетную запись tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Выберите подписку hello требуется toocreate канал ExpressRoute.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Создайте канал ExpressRoute.

  Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-arm.md) и их подготовки с помощью поставщика услуг подключения hello.

  Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас. В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello. Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.
3. Проверьте hello tooensure цепь ExpressRoute подготовленный и также включена. Используйте следующий пример hello.

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  Hello ответ — аналогично toohello в следующем примере:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Настройка открытого пиринга Azure для hello схемы. Убедитесь, что следующие сведения, прежде чем продолжить дальнейшей hello.

  * / 30 подсеть для основной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4.
  * / 30 подсеть для дополнительной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4.
  * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
  * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS.
  * **Необязательно —** хэш MD5 при выборе toouse один.

  Запустите следующий пример tooconfigure Azure открытый пиринг для своего канала hello

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  При выборе toouse хэш MD5, используйте следующий пример hello:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.
  > 
  >

### <a name="tooview-azure-public-peering-details"></a>tooview открытый пиринг сведения о Azure

Можно получить сведения о конфигурации, с помощью hello, выполнив командлет:

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate конфигурации открытого пиринга Azure

Вы можете обновить любая часть конфигурации hello, используя следующий пример hello. В этом примере выполняется обновление hello VLAN ID канала hello из 200 too600.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a>toodelete частного пиринга Azure

Пиринг конфигурации можно удалить, выполнив следующий пример hello.

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a>Пиринг Майкрософт

Этот раздел поможет вам создать, получить, обновление и удаление пиринга конфигурации Microsoft hello за канал ExpressRoute.

> [!IMPORTANT]
> Microsoft пиринг ExpressRoute каналов, которые были настроены предыдущих tooAugust 1, 2017 г. будет иметь все службы префиксов, объявленных через пиринг Майкрософт hello, даже если не определены фильтры маршрутов. Пиринг каналы ExpressRoute, настроенных в течение или после 1 августа 2017 г. Корпорация Майкрософт не будет иметь префиксы объявленных пока фильтр не будет подключено toohello канала. Дополнительные сведения см. в руководстве по [настройке фильтра маршрута для пиринга Майкрософт](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate пиринг Майкрософт

1. Импортируйте модуль PowerShell hello для ExpressRoute.

  Необходимо установить установщик последнюю PowerShell hello из [коллекции PowerShell](http://www.powershellgallery.com/) и импортируйте модули диспетчера ресурсов Azure hello в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello. Вам потребуется toorun PowerShell с правами администратора.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  Импортируйте все модули AzureRM.* hello внутри hello известный диапазон версию семантики.

  ```powershell
  Import-AzureRM
  ```

  Можно импортировать также просто выберите модуль внутри hello известный диапазон версию семантики.

  ```powershell
  Import-Module AzureRM.Network
  ```

  Войдите в учетную запись tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Выберите подписку hello требуется toocreate канал ExpressRoute.

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Создайте канал ExpressRoute.

  Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-arm.md) и их подготовки с помощью поставщика услуг подключения hello.

  Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас. В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello. Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.
3. Убедитесь, что подготовлены, а также включить toomake цепь ExpressRoute hello. Используйте следующий пример hello.

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  Hello ответ — аналогично toohello в следующем примере:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Настройка Microsoft пиринг для цепи hello. Убедитесь, что hello следующую информацию, прежде чем продолжить.

  * / 30 подсеть для основной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.
  * / 30 подсеть для дополнительной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.
  * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
  * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS.
  * Объявленные префиксы: необходимо предоставить список всех префиксов планирование tooadvertise сеансом BGP hello. Допускаются только общедоступные префиксы IP-адресов. Если планируется toosend набор префиксов, вы можете отправить список с разделителями запятыми. Эти префиксы должны быть tooyou, зарегистрированные в RIR / IRR.
  * **Необязательно —** клиента ASN: если префиксы рекламы, не зарегистрированный toohello пиринг как число, можно указать hello в качестве номера toowhich они зарегистрированы.
  * Имя реестра маршрутизации: Можно указать hello RIR / IRR, для какой hello, а число и префиксы зарегистрирована.
  * **Необязательно —** хэш MD5 при выборе toouse один.

   Используйте следующие пиринг Майкрософт пример tooconfigure для своего канала hello.

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a>данные пиринга tooget Microsoft

Можно получить сведения о конфигурации, используя следующий пример hello:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a>Конфигурация пиринга Майкрософт tooupdate

Можно обновить любая часть конфигурации hello, используя следующий пример hello.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a>toodelete пиринг Майкрософт

Пиринг конфигурации можно удалить, выполнив следующий командлет hello.

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a>Дальнейшие действия

Следующий шаг [связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-arm.md).

* Дополнительную информацию о рабочих процессах ExpressRoute см. в статье [Процедуры ExpressRoute для подготовки каналов и состояний каналов](expressroute-workflows.md).
* Дополнительную информацию о пиринге канала см. в статье [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).
* Подробнее о работе с виртуальными сетями см. в статье [Обзор виртуальных сетей](../virtual-network/virtual-networks-overview.md).
