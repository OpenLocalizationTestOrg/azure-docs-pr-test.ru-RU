---
title: "Примеры конфигурации маршрутизатора клиента aaaExpressRoute | Документы Microsoft"
description: "Эта страница содержит примеры конфигурации для маршрутизаторов серий Cisco ASA и Juniper MX."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 5c91f24e6082e01c3e8df91b4fcfda46a6c29fa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a>Конфигурация маршрутизатора образцы tooset вверх и управлять маршрутизацией
Эта страница содержит примеры конфигурации интерфейса и маршрутизации для маршрутизаторов серий Cisco IOS-XE и Juniper MX. Эти примеры предполагаемого toobe только рекомендации и не должны использоваться как есть. Можно работать с вашего поставщика toocome с соответствующие настройки для вашей сети. 

> [!IMPORTANT]
> Образцы на этой странице, предполагаемой toobe исключительно для рекомендации. Необходимо работать с у поставщика продаж / технической группы и вашей сети team toocome вверх с toomeet соответствующие настройки вашим потребностям. Корпорация Майкрософт не будет поддерживать проблемы связанные tooconfigurations, перечисленные на этой странице. Для получения поддержки вам необходимо обратиться к поставщику устройства.
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a>Параметры MTU и TCP MSS в интерфейсах маршрутизатора
* Hello MTU для интерфейса ExpressRoute hello равно 1500, что hello обычно по умолчанию используется значение MTU для интерфейса Ethernet на маршрутизаторе. Если маршрутизатор имеет другой MTU по умолчанию, нет toospecify нет необходимости значение на интерфейс маршрутизатора hello.
* В отличие от шлюза VPN Azure hello TCP MSS за канал ExpressRoute toobe указан не требуются.

Ниже примеров конфигурации маршрутизатора применяются tooall пиринги. Для получения дополнительных сведений о маршрутизации обратитесь к статьям [Сеансы пиринга ExpressRoute](expressroute-circuit-peerings.md) и [Требования ExpressRoute к маршрутизации](expressroute-routing.md).


## <a name="cisco-ios-xe-based-routers"></a>Маршрутизаторы на основе Cisco IOS-XE
Hello образцы в этом разделе применяются для любой маршрутизатором, работающим под управлением семейства ОС IOS XE hello.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Настройка интерфейсов и дочерние интерфейсы
Вам потребуется дочерний интерфейс на пиринг в каждый маршрутизатор подключить tooMicrosoft. Дочерний интерфейс можно идентифицировать с помощью идентификатора виртуальной локальной сети или с помощью накопленной пары идентификаторов виртуальных сетей и IP-адреса.

**Определение интерфейса Dot1Q**

Этот образец представляет определение интерфейс hello интерфейс с одним идентификатором виртуальной локальной сети. Hello VLAN ID является уникальным для каждого пиринга. последний октет Hello IPv4-адрес всегда будет нечетным числом.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

**Определение интерфейса QinQ**

Этот образец предоставляет определение интерфейс hello для вложенных интерфейса с помощью двух идентификаторов виртуальных ЛС. Привет, остается внешней VLAN ID (s тегов), если используется hello же через все пиринги hello. Hello внутренний идентификатор виртуальной локальной сети (c-tag) уникальным для каждого пиринга. последний октет Hello IPv4-адрес всегда будет нечетным числом.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a>2. Настройка сеансов eBGP
Для каждого пиринга необходимо настроить сеанс BGP с Майкрософт. Образец Hello ниже включает toosetup сеанс BGP с корпорацией Майкрософт. Если hello IPv4-адрес, используемый для интерфейса sub a.b.c.d, hello IP-адрес BGP hello окружения (Майкрософт) будет a.b.c.d+1. последний октет Hello адреса IPv4 соседний узел BGP hello всегда будет четное число.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Настройка toobe префиксов, объявленных сеансом BGP hello
Вы можете настроить ваш tooMicrosoft выберите префиксы tooadvertise маршрутизатора. Это можно сделать с помощью пример "hello".

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a>4. Карты маршрутизации
Вы можете использовать карты маршрута и префикс перечислены префиксы toofilter распространены в вашей сети. Можно использовать образец hello ниже tooaccomplish задачу hello. Убедитесь, что вы задали соответствующие настройки списков префиксов.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a>Маршрутизаторы серии Juniper MX
Hello образцы в этом разделе применяются для ряда маршрутизаторы Juniper MX.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Настройка интерфейсов и дочерние интерфейсы

**Определение интерфейса Dot1Q**

Этот образец представляет определение интерфейс hello интерфейс с одним идентификатором виртуальной локальной сети. Hello VLAN ID является уникальным для каждого пиринга. последний октет Hello IPv4-адрес всегда будет нечетным числом.

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


**Определение интерфейса QinQ**

Этот образец предоставляет определение интерфейс hello для вложенных интерфейса с помощью двух идентификаторов виртуальных ЛС. Привет, остается внешней VLAN ID (s тегов), если используется hello же через все пиринги hello. Hello внутренний идентификатор виртуальной локальной сети (c-tag) уникальным для каждого пиринга. последний октет Hello IPv4-адрес всегда будет нечетным числом.

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a>2. Настройка сеансов eBGP
Для каждого пиринга необходимо настроить сеанс BGP с Майкрософт. Образец Hello ниже включает toosetup сеанс BGP с корпорацией Майкрософт. Если hello IPv4-адрес, используемый для интерфейса sub a.b.c.d, hello IP-адрес BGP hello окружения (Майкрософт) будет a.b.c.d+1. последний октет Hello адреса IPv4 соседний узел BGP hello всегда будет четное число.

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Настройка toobe префиксов, объявленных сеансом BGP hello
Вы можете настроить ваш tooMicrosoft выберите префиксы tooadvertise маршрутизатора. Это можно сделать с помощью пример "hello".

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a>4. Карты маршрутизации
Вы можете использовать карты маршрута и префикс перечислены префиксы toofilter распространены в вашей сети. Можно использовать образец hello ниже tooaccomplish задачу hello. Убедитесь, что вы задали соответствующие настройки списков префиксов.

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a>Дальнейшие действия
В разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md) для получения дополнительных сведений.

