---
title: "Как tooconfigure маршрутизации (пиринг) для канала ExpressRoute: Azure: классический | Документы Microsoft"
description: "В этой статье содержится описание этапов hello для создания и подготовки hello private, public и Microsoft пиринг канал ExpressRoute. В этой статье также рассказывается, как состояние toocheck hello, обновления или удаления пиринги для своего канала."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a>Создание и изменение пиринга для канала ExpressRoute (классическая модель)
> [!div class="op_single_selector"]
> * [Портал Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Интерфейс командной строки Azure](howto-routing-cli.md)
> * [Видео — частный пиринг](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Видео — общедоступный пиринг](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Видео — пиринг Майкрософт](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (классическая модель)](expressroute-howto-routing-classic.md)
> 

Данная статья поможет выполнить шаги toocreate hello и управление конфигурацией маршрутизации для канала ExpressRoute с помощью PowerShell и hello классической модели развертывания. Hello шаги также отображается как toocheck hello состояния, обновление, или удалить и отзыв пиринги за канал ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**О моделях развертывания Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a>Предварительные требования для настройки
* Вам потребуется hello последнюю версию hello командлеты PowerShell Azure службы управления (SM). Дополнительные сведения см. в разделе [Приступая к работе с командлетами Azure PowerShell](/powershell/azure/overview).  
* Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md) страницы hello [требования к маршрутизации](expressroute-routing.md) страницы и hello [рабочих процессов](expressroute-workflows.md) страницы перед началом настройки.
* Вам потребуется активный канал ExpressRoute. Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-classic.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить. Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен для вас toobe может toorun hello командлетов, описанных ниже.

> [!IMPORTANT]
> Эти инструкции применяются только toocircuits, созданных с помощью предложения службы связи уровня 2 поставщиков услуг. Если вы работаете с поставщиком, предлагающим услуги третьего уровня (обычно IPVPN, типа MPLS), ваш поставщик услуг подключения выполнит настройку и управление конфигурацией самостоятельно.
> 
> 

Для каждого канала ExpressRoute можно настроить один, два или три пиринга (частный пиринг Azure, общедоступный пиринг Azure и пиринг Microsoft). Пиринги можно настраивать в любом порядке, Тем не менее необходимо выполнить настройку hello из каждого из них пиринга одновременно.


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a>Войдите в tooyour учетная запись Azure и выберите подписку
1. Откройте консоль PowerShell с повышенными правами и подключите tooyour учетную запись. Используйте следующий пример toohelp подключении hello.

        Login-AzureRmAccount

2. Проверьте hello подписки для учетной записи hello.

        Get-AzureRmSubscription

3. При наличии нескольких подписок выберите подписку hello, что требуется toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Затем используйте следующий командлет tooadd hello tooPowerShell вашей подписки Azure для hello классической модели развертывания.

        Add-AzureAccount


## <a name="azure-private-peering"></a>Частный пиринг Azure
В этом разделе описано, как toocreate, получение, обновление и удаление hello Azure закрытая конфигурация пиринга канал ExpressRoute. 

### <a name="toocreate-azure-private-peering"></a>toocreate открытого пиринга Azure
1. **Импортируйте модуль PowerShell hello для ExpressRoute.**
   
    Модули Azure и ExpressRoute hello необходимо импортировать в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello. Выполнения hello следующими командами tooimport hello Azure и ExpressRoute модулей в сеанс PowerShell hello.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Создайте канал ExpressRoute.**
   
    Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-classic.md) и их подготовки с помощью поставщика услуг подключения hello. Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас. В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello. Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, выполните приведенные ниже инструкции hello. 
3. **Проверьте tooensure цепь ExpressRoute hello, его инициализации.**
   
    Если hello канал ExpressRoute подготовлены и включены также необходимо отметить toosee. См. ниже пример hello.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Убедитесь, что hello цепь подготовлена и включен. Если это не так, работаете с вашей tooget поставщика подключения канала требуется toohello состояние и состояние.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Настройка открытого пиринга Azure для hello схемы.**
   
    Убедитесь, что hello следующих элементов, прежде чем продолжить hello следующие шаги:
   
   * / 30 подсеть для основной ссылки hello. Она не должна входить в адресное пространство, зарезервированное для виртуальных сетей.
   * / 30 подсеть для дополнительной ссылки hello. Она не должна входить в адресное пространство, зарезервированное для виртуальных сетей.
   * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
   * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS. Для этого пиринга можно использовать частный номер AS. Не используйте номер 65515.
   * Хэш MD5 при выборе toouse один. **Это необязательно**.
     
    Можно выполнить следующий командлет tooconfigure открытого пиринга Azure для своего канала hello.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100
     
    При выборе toouse хэш MD5, можно использовать командлет hello ниже.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure закрытого пиринга подробные сведения
Можно получить сведения о конфигурации, с помощью hello, выполнив командлет

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate конфигурации закрытого пиринга Azure
Можно обновить любой части hello конфигурации, с помощью hello, выполнив командлет. В следующем примере hello hello VLAN ID канала hello обновляется из 100 too500.

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a>toodelete открытого пиринга Azure
Можно удалить пиринг конфигурацию, выполнив следующий командлет hello.

> [!WARNING]
> Необходимо убедиться, что все виртуальные сети будут отключены от hello канал ExpressRoute перед выполнением этого командлета. 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a>Общедоступный пиринг Azure
В этом разделе описано, как toocreate, получение, обновление и удаление hello Azure открытая конфигурация пиринга канал ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate частного пиринга Azure
1. **Импортируйте модуль PowerShell hello для ExpressRoute.**
   
    Модули Azure и ExpressRoute hello необходимо импортировать в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello. Выполнения hello следующими командами tooimport hello Azure и ExpressRoute модулей в сеанс PowerShell hello. 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Создание канала ExpressRoute**
   
    Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-classic.md) и их подготовки с помощью поставщика услуг подключения hello. Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure открытый пиринг для вас. В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello. Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, выполните приведенные ниже инструкции hello.
3. **Проверьте tooensure цепь ExpressRoute, он предоставляется**
   
    Если hello канал ExpressRoute подготовлены и включены также необходимо отметить toosee. См. ниже пример hello.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Убедитесь, что hello цепь подготовлена и включен. Если это не так, работаете с вашей tooget поставщика подключения канала требуется toohello состояние и состояние.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Настройка открытого пиринга Azure для схемы hello**
   
    Убедитесь, что hello следующую информацию, прежде чем продолжить, далее.
   
   * / 30 подсеть для основной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4.
   * / 30 подсеть для дополнительной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4.
   * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
   * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS.
   * Хэш MD5 при выборе toouse один. **Это необязательно**.
     
    Можно выполнить следующий командлет tooconfigure открытого пиринга Azure для своего канала hello
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200
     
    При выборе toouse MD5-хэш можно использовать командлет hello
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a>tooview открытый пиринг сведения о Azure
Можно получить сведения о конфигурации, с помощью hello, выполнив командлет

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate конфигурации открытого пиринга Azure
Можно обновить любой части hello конфигурации, с помощью hello, выполнив командлет

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

Hello VLAN ID канала hello обновляется из 200 too600 в hello в предыдущем примере.

### <a name="toodelete-azure-public-peering"></a>toodelete частного пиринга Azure
Можно удалить пиринг конфигурацию, выполнив следующий командлет hello

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a>Пиринг Майкрософт
В этом разделе описано, как toocreate, получения, обновления и удаления конфигурации пиринг Microsoft hello за канал ExpressRoute. 

### <a name="toocreate-microsoft-peering"></a>toocreate пиринг Майкрософт
1. **Импортируйте модуль PowerShell hello для ExpressRoute.**
   
    Модули Azure и ExpressRoute hello необходимо импортировать в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello. Выполнения hello следующими командами tooimport hello Azure и ExpressRoute модулей в сеанс PowerShell hello.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Создание канала ExpressRoute**
   
    Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-classic.md) и их подготовки с помощью поставщика услуг подключения hello. Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас. В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello. Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, выполните приведенные ниже инструкции hello.
3. **Проверьте tooensure цепь ExpressRoute, он предоставляется**
   
    Сначала необходимо проверить toosee, если hello канал ExpressRoute находится в состоянии подготовлена и включен.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Убедитесь, что hello цепь подготовлена и включен. Если это не так, работаете с вашей tooget поставщика подключения канала требуется toohello состояние и состояние.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Настройка Microsoft пиринг для цепи hello**
   
    Убедитесь, что hello следующую информацию, прежде чем продолжить.
   
   * / 30 подсеть для основной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.
   * / 30 подсеть для дополнительной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.
   * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
   * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS.
   * Объявленные префиксы: необходимо предоставить список всех префиксов планирование tooadvertise сеансом BGP hello. Допускаются только общедоступные префиксы IP-адресов. Если планируется toosend набор префиксов можно отправить список разделенных запятыми. Эти префиксы должны быть tooyou, зарегистрированные в RIR / IRR.
   * Клиент ASN: Если вы размещаете рекламу, не зарегистрированный toohello пиринг как число префиксов, можно указать hello как число toowhich их регистрации. **Это необязательно**.
   * Имя реестра маршрутизации: Можно указать hello RIR / IRR, для какой hello, а число и префиксы зарегистрирована.
   * Хэш MD5, при выборе toouse один. **Это необязательно.**
     
    Можно выполнить следующий командлет tooconfigure Microsoft pering для своего канала hello
     
        New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="tooview-microsoft-peering-details"></a>данные пиринга tooview Microsoft
Можно получить сведения о конфигурации, используя следующий командлет hello.

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a>Конфигурация пиринга Майкрософт tooupdate
Можно обновить любой части hello конфигурации, с помощью hello, выполнив командлет.

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a>toodelete пиринг Майкрософт
Можно удалить пиринг конфигурацию, выполнив следующий командлет hello.

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a>Дальнейшие действия
Далее, [связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-classic.md).

* Дополнительные сведения о рабочих процессах см. в разделе [Рабочие процессы ExpressRoute](expressroute-workflows.md).
* Дополнительную информацию о пиринге канала см. в статье [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).

