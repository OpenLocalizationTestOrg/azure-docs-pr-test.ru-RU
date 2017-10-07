---
title: "Проверка подключения. Руководство по устранению неполадок Azure ExpressRoute | Документация Майкрософт"
description: "Эта страница содержит инструкции Устранение неполадок и проверка подключения tooend end из канала ExpressRoute."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a>Проверка подключения ExpressRoute
ExpressRoute, которая расширяет локальную сеть в облако Microsoft hello через подключение к частной, можно добиться с помощью поставщика услуг подключения, включает в себя следующие три различных сетевых зоны hello.

-   клиентскую сеть;
-   сеть поставщика;
-   центр обработки данных Майкрософт.

Hello цель данного документа — tooidentify пользователя toohelp где (или даже в том случае, если) существует проблема с подключением и в пределах зоны, тем самым tooseek помощь в соответствующую группу tooresolve hello проблему. Если службу технической поддержки Майкрософт необходимые tooresolve проблему, откройте запрос в службу поддержки с [поддержки Майкрософт][Support].

> [!IMPORTANT]
> Данный документ является предполагаемым toohelp диагностики и исправления простой проблемы. Это не toobe предназначен для замены технической поддержки Майкрософт. Откройте запрос в службу поддержки с [поддержки Майкрософт] [ Support] Если проблему не удается toosolve hello, с помощью hello инструкциям.
>
>

## <a name="overview"></a>Обзор
Hello следующей схеме показаны подключения логических hello сети tooMicrosoft сети клиента с помощью ExpressRoute.
[![1]][1]

В предшествующей схеме hello hello числа указывают точки ключа сети. Hello точке сети часто ссылки в этой статье на их соответствующее число.

В зависимости от подключения ExpressRoute hello модели (совместного размещения в облаке Exchange, Ethernet-подключение между узлами или Any к any (IPVPN)) hello сети точки 3 и 4 могут быть коммутаторы (уровень 2 устройства). точки ключа сетевой Hello показано выглядят следующим образом:

1.  Клиентское вычислительное устройство (например, сервер или компьютер).
2.  Клиентские пограничные маршрутизаторы (CE). 
3.  Пограничные маршрутизаторы (коммутаторы) поставщика услуг связи, подключенные к клиентским пограничным маршрутизаторам (PE, подключенные к CE). Ссылка tooas PE CEs в этом документе.
4.  Пограничные маршрутизаторы (коммутаторы) поставщика услуг связи, подключенные к MSEE. Ссылка tooas PE MSEEs в этом документе.
5.  Маршрутизаторы MSEE ExpressRoute.
6.  Шлюз виртуальной сети
7.  Вычислений устройства на hello виртуальной сети Azure

При использовании модели подключения к совместного размещения в облаке Exchange или Ethernet-подключение точка-точка hello пограничный маршрутизатор клиента hello (2) породит BGP пиринг с MSEEs (5). Точки сети 3 и 4 будут по-прежнему существовать, но будут в некоторой степени прозрачными как устройства уровня 2.

При использовании модели подключения к любой к any (IPVPN) hello hello синтаксические ошибки (с выходом MSEE) (4) породит BGP пиринг с MSEEs (5). Маршруты затем распространит задней toohello сети клиента через сети поставщика услуг IPVPN hello.

>[!NOTE]
>Для обеспечения высокой доступности ExpressRoute корпорации Майкрософт необходима избыточная пара сеансов BGP между маршрутизаторами MSEE (5) и маршрутизаторами поставщика услуг связи, подключенными к MSEE (PE-MSEE) (4). Рекомендуется также избыточная пара сетевых путей между клиентской сетью и маршрутизаторами PE-CE. Однако в модели подключения Any к any (IPVPN) одно устройство CE (2) возможно подключенных tooone или дополнительные синтаксические ошибки (3).
>
>

(с точки сети hello обозначается hello связанный номер) рассматриваются toovalidate канал ExpressRoute hello следующие шаги:
1. [Проверить подготовку и состояние канала (5).](#validate-circuit-provisioning-and-state)
2. [Проверить, что настроен по крайней мере один пиринг ExpressRoute (5).](#validate-peering-configuration)
3. [Проверка ARP между Майкрософт и hello поставщика услуг (связь между 4 и 5)](#validate-arp-between-microsoft-and-the-service-provider)
4. [Проверка BGP и маршрутов на hello MSEE (BGP между 4 too5 и 5 too6, если подключение виртуальной сети)](#validate-bgp-and-routes-on-the-msee)
5. [Проверьте hello статистике трафика (трафик, проходящий через 5)](#check-the-traffic-statistics)

Дополнительные проверки и проверки будет добавлена в hello в будущем, посетите страницу ежемесячно!

##<a name="validate-circuit-provisioning-and-state"></a>Проверка подготовки и состояния канала
Независимо от модели подключения к hello, канал ExpressRoute имеет toobe создан и, следовательно, службу создан для подготовки ключа. При подготовке канала ExpressRoute устанавливаются избыточные подключения уровня 2 между маршрутизаторами PE-MSEE (4) и MSEE (5). Дополнительные сведения о том, как toocreate, изменять, предоставить и проверить канал ExpressRoute. в статье hello [Создание и изменение канал ExpressRoute][CreateCircuit].

>[!TIP]
>Ключ службы однозначно идентифицирует канал ExpressRoute. Этот ключ является обязательным для большинства команд powershell hello, упомянутые в этом документе. Кроме того, следует вам нужна помощь от корпорации Майкрософт или из tootroubleshoot партнера ExpressRoute проблему ExpressRoute обслуживает hello ключа tooreadily идентификации hello канала.
>
>

###<a name="verification-via-hello-azure-portal"></a>Проверка через портал Azure hello
В hello портал Azure, можно проверить состояние hello канал ExpressRoute, выбрав ![2][2] на hello левой боковой панели меню, а затем выбрав hello канал ExpressRoute. Выбор ExpressRoute цепи, перечисленных в разделе «Всех ресурсов» открывает колонку цепь ExpressRoute hello. В hello ![3][3] раздел hello колонке hello essentials отображается, как показано на следующий снимок экрана приветствия ExpressRoute:

![4][4]    

В ExpressRoute Essentials hello *Circuit состояние* указывает состояние hello hello канала на стороне Microsoft hello. *Поставщик состояния* указывает, был ли цепи hello *инициализировано или не подготовлены* на стороне поставщика услуг hello. 

ExpressRoute канала toobe оперативной, hello *Circuit состояние* должно быть *включено* и hello *состояние поставщика* должно быть *инициализировано*.

>[!NOTE]
>Если hello *Circuit состояние* — не включено, обратитесь в службу [поддержки Майкрософт][Support]. Если hello *состояние поставщика* — не подготовлено, обратитесь к поставщику услуг.
>
>

###<a name="verification-via-powershell"></a>Проверка с помощью PowerShell
toolist все hello каналов ExpressRoute в группе ресурсов, выполните следующую команду hello.

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
>Имя группы ресурсов можно получить с помощью портала Azure hello. Обратитесь к подразделу предыдущих hello в этом документе и обратите внимание, что имя группы ресурсов hello, указан снимок экрана примера hello.
>
>

tooselect конкретного канала ExpressRoute в группе ресурсов hello используйте следующую команду:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

Пример ответа:

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

tooconfirm, если канал ExpressRoute работоспособна, Обратите особое внимание toohello следующие поля:

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
>Если hello *параметр* — не включено, обратитесь в службу [поддержки Майкрософт][Support]. Если hello *ServiceProviderProvisioningState* — не подготовлено, обратитесь к поставщику услуг.
>
>

###<a name="verification-via-powershell-classic"></a>Проверка с помощью PowerShell (классическая модель)
toolist все hello каналов ExpressRoute в подписке, выполните следующую команду hello.

    Get-AzureDedicatedCircuit

tooselect конкретного канала ExpressRoute, hello используйте следующую команду:

    Get-AzureDedicatedCircuit -ServiceKey **************************************

Пример ответа:

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

tooconfirm, если канал ExpressRoute находится в рабочем состоянии, Обратите особое внимание toohello следующие поля: ServiceProviderProvisioningState: состояние подготовки: включено

>[!NOTE]
>Если hello *состояние* — не включено, обратитесь в службу [поддержки Майкрософт][Support]. Если hello *ServiceProviderProvisioningState* — не подготовлено, обратитесь к поставщику услуг.
>
>

##<a name="validate-peering-configuration"></a>Проверка настройки пиринга
После завершенного hello подготовки канал ExpressRoute hello hello поставщика услуг через hello канал ExpressRoute между MSEE-PR (4) и MSEEs (5) можно создать конфигурации маршрутизации. Каждый канал ExpressRoute может иметь одно, два или три контексты маршрутизации включен: открытого пиринга Azure (трафик tooprivate виртуальных сетей в Azure), открытого пиринга Azure (IP-toopublic трафика адреса в Azure) и (трафик tooOffice 365 пиринг Майкрософт и Dynamics 365). Дополнительные сведения о том, как toocreate и изменить конфигурацию маршрутизации, см. в статье hello [Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering].

###<a name="verification-via-hello-azure-portal"></a>Проверка через портал Azure hello
>[!IMPORTANT]
>В hello портал Azure, при котором пиринги ExpressRoute, имеется известная ошибка *не* отображаются на портале hello, если настроен поставщиком услуг hello. Добавление пиринги ExpressRoute через портал hello или PowerShell *перезаписывает параметры поставщика службы hello*. Это действие прерывает hello маршрутизации на канал ExpressRoute hello и требуется поддержка hello параметров hello toorestore поставщика службы hello и восстановить нормальную маршрутизацию. Измените hello ExpressRoute пиринги только в том случае, если известно, что поставщик услуг, hello предоставляет только 2 уровня служб!
>
>

<p/>
>[!NOTE]
>Если предоставлен уровня 3 с hello службы поставщика и hello пиринги пусты портале hello, PowerShell может быть используется toosee hello службы настроены параметры поставщика.
>
>

В hello портал Azure, можно проверить состояние канала ExpressRoute, выбрав ![2][2] на hello левой боковой панели меню, а затем выбрав hello канал ExpressRoute. Выбор ExpressRoute цепи, перечисленных в разделе «Всех ресурсов» будет открыт колонке цепь ExpressRoute hello. В hello ![3][3] раздел hello колонке hello ExpressRoute, могут быть указаны essentials, как показано на следующий снимок экрана приветствия:

![5][5]

В предыдущих пример hello как отмечено выше Azure закрытого пиринга маршрутизации контекста включен, в то время как открытые Azure и контексты маршрутизации пиринга Майкрософт не включен. Успешно включен пиринга контекст также будет иметь подсетей основного и дополнительного точка-точка (требуется для протокола BGP) hello в списке. Hello /30 подсети используются для IP-адрес интерфейса hello hello MSEEs и PE MSEEs. 

>[!NOTE]
>Если пиринг не включена, убедитесь, если hello первичного и вторичного подсети назначены соответствуют конфигурации hello в PE-MSEEs. Если нет, toochange hello конфигурации в MSEE маршрутизаторы, см. слишком[Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering]
>
>

###<a name="verification-via-powershell"></a>Проверка с помощью PowerShell
tooget hello Azure закрытого пиринга сведения о конфигурации, используйте hello, следующие команды:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

Пример ответа в случае успешной настройки частного пиринга:

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 Успешно включен пиринга контекста будет иметь префиксов адреса основного и дополнительного hello в списке. Hello /30 подсети используются для IP-адрес интерфейса hello hello MSEEs и PE MSEEs.

tooget hello Azure открытый пиринг сведения о конфигурации, используйте hello, следующие команды:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

tooget hello Microsoft пиринга сведения о конфигурации, используйте hello, следующие команды:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

Если пиринг не настроен, отобразится сообщение об ошибке. Образец ответа, когда hello указано пиринга (Azure открытый пиринг в этом примере) настроен в цепи hello:

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
>Если пиринг не включена, проверьте при конфигурации hello подсетей основного и дополнительного назначенный соответствия hello на hello связаны PE MSEE. Также проверьте наличие hello исправить *VlanId*, *AzureASN*, и *PeerASN* применяются MSEEs и если эти значения сопоставляет toohello те на hello связаны PE MSEE. Если вы выбрали хэширования MD5 hello общего ключа должны совпадать на пару MSEE и PE MSEE. конфигурации hello toochange на маршрутизаторах MSEE hello, см. слишком [создание и изменение маршрутизации для канала ExpressRoute] [CreatePeering].  
>
>

### <a name="verification-via-powershell-classic"></a>Проверка с помощью PowerShell (классическая модель)
tooget hello Azure закрытого пиринга сведения о конфигурации, используйте hello следующую команду:

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

Пример ответа в случае успешной настройки частного пиринга:

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

Объект успешно, включен пиринга контекста будет иметь подсетей основного и дополнительного одноранговых hello в списке. Hello /30 подсети используются для IP-адрес интерфейса hello hello MSEEs и PE MSEEs.

tooget hello Azure открытый пиринг сведения о конфигурации, используйте hello, следующие команды:

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

tooget hello Microsoft пиринга сведения о конфигурации, используйте hello, следующие команды:

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
>Если пиринги уровня 3, заданные поставщиком услуг hello, установка hello пиринги ExpressRoute через портал hello или PowerShell перезаписывает hello параметры поставщика службы. Сброс параметров пиринга стороне поставщика hello требуется поддержка hello hello поставщика услуг. Измените hello ExpressRoute пиринги только в том случае, если известно, что поставщик услуг, hello предоставляет только 2 уровня служб!
>
>

<p/>
>[!NOTE]
>Если пиринг не включена, проверьте при конфигурации hello первичного и вторичного одноранговых подсети назначены соответствия hello на hello связаны PE MSEE. Также проверьте наличие hello исправить *VlanId*, *AzureAsn*, и *PeerAsn* применяются MSEEs и если эти значения сопоставляет toohello те на hello связаны PE MSEE. конфигурации hello toochange на маршрутизаторах MSEE hello, см. слишком [создание и изменение маршрутизации для канала ExpressRoute] [CreatePeering].
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a>Проверка ARP между Майкрософт и hello поставщика услуг
В этом разделе используются классические команды PowerShell. Если вы использовали команды PowerShell диспетчера ресурсов Azure, убедитесь, что доступ администратору или соадминистратору подписки toohello через [классический портал Azure][OldPortal]. Устранение неполадок с помощью диспетчера ресурсов Azure команды можно найти toohello [начало ARP таблиц в модели развертывания диспетчера ресурсов hello] [ ARP] документа.

>[!NOTE]
>можно использовать tooget ARP hello портал Azure и команд PowerShell диспетчера ресурсов Azure. При обнаружении ошибки с помощью команд PowerShell диспетчера ресурсов Azure hello, классический команд PowerShell должны работать в качестве классического PowerShell команды также работать с каналами ExpressRoute диспетчера ресурсов Azure.
>
>

tooget hello таблицы ARP от основного маршрутизатора MSEE hello для частного пиринга hello, выполните следующую команду hello.

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Пример ответа для команды hello, в случае успешного hello:

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

Аналогичным образом, можно проверить таблицы ARP из hello MSEE в hello hello *основной*/*получателя* пути, для *закрытый* /  *Открытый*/*Microsoft* пиринги.

Hello следующий пример, показано hello ответа hello команды для пиринга не существует.

    ARP Info:
       
>[!NOTE]
>Если hello таблицы ARP отсутствует IP-адресов интерфейсов hello сопоставляются tooMAC адреса, hello просмотрите следующую информацию:
>1. Если назначена hello первый IP-адрес подсети hello /30 для hello связь между hello MSEE PR и MSEE используется в интерфейсе hello MSEE PR. Azure всегда использует hello второй IP-адрес для MSEEs.
>2. Убедитесь, если hello клиента (C-тег) и теги VLAN службы (S-Tag) соответствуют на пару MSEE PR и MSEE.
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a>Проверка BGP и маршрутов на hello MSEE
В этом разделе используются классические команды PowerShell. Если вы использовали команды PowerShell диспетчера ресурсов Azure, убедитесь, что доступ администратору или соадминистратору подписки toohello через [классический портал Azure][OldPortal]

>[!NOTE]
>tooget BGP сведения, оба hello, можно использовать команды PowerShell диспетчера ресурсов Azure и портала Azure. При обнаружении ошибки с помощью команд PowerShell диспетчера ресурсов Azure hello, классический команд PowerShell должны работать в качестве классического PowerShell команды также работать с каналами ExpressRoute диспетчера ресурсов Azure.
>
>

tooget hello таблицу маршрутизации (BGP сосед) сводки для определенного контекста маршрутизации, выполните следующую команду hello.

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

Пример ответа:

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

Как показано в предшествующих пример hello, команда hello является полезным toodetermine для длительность установки контекста маршрутизации hello. Также указывается число префиксов маршрутов объявлены пиринга маршрутизатором hello.

>[!NOTE]
>Если состояние hello в активной работы или простоя, проверьте при конфигурации hello первичного и вторичного одноранговых подсети назначены соответствия hello на hello связаны PE MSEE. Также проверьте наличие hello исправить *VlanId*, *AzureAsn*, и *PeerAsn* применяются MSEEs и если эти значения сопоставляет toohello те на hello связаны PE MSEE. Если вы выбрали хэширования MD5 hello общего ключа должны совпадать на пару MSEE и PE MSEE. конфигурации hello toochange на маршрутизаторах MSEE hello, см. слишком[Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering].
>
>

<p/>
>[!NOTE]
>Если определенные назначения недоступны через определенный пиринг, проверьте hello таблицы маршрутов из MSEEs hello, принадлежащие данному контексту пиринга toohello. Если соответствующий префикс (возможно, NATed IP) присутствует в таблице маршрутизации hello, затем проверьте существуют брандмауэры, ACL или NSG по пути hello и разрешать или запрещать трафик hello.
>
>

tooget hello полной таблицы маршрутизации из MSEE hello *основной* путь для конкретного hello *закрытый* маршрутизации контекста, hello используйте следующую команду:

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Пример успешный результат для hello команды является:

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

Аналогичным образом, можно проверить таблицы маршрутизации hello из hello MSEE в hello *основной*/*получателя* пути, для *закрытый* / *Открытый*/*Microsoft* пиринга контекста.

Hello следующий пример, показано hello ответа hello команды для пиринга не существует:

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a>Проверьте hello статистики
tooget hello вместе статистике трафика основной и дополнительный путь--байт и выхода из системы--пиринга контекста hello используйте следующую команду:

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

Пример выходных данных команды hello является:

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

Пример выходных данных команды hello для пиринга несуществующий является:

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a>Дальнейшие действия
Для получения дополнительных сведений справки ознакомьтесь с hello ссылкам:

- [Служба технической поддержки Майкрософт][Support]
- [Создание и изменение канала ExpressRoute][CreateCircuit]
- [Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering]

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Логическое подключение ExpressRoute"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Значок "Все ресурсы""
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Значок "Обзор""
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Снимок экран раздела с основными сведениями об ExpressRoute"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Снимок экран раздела с основными сведениями об ExpressRoute"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






