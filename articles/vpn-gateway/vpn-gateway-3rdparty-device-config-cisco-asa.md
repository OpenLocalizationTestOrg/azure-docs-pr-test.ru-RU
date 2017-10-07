---
title: "Конфигурация aaaSample - устройств Cisco ASA подключение VPN-шлюзов tooAzure | Документы Microsoft"
description: "Эта статья содержит пример конфигурации для устройств Cisco ASA подключение tooAzure VPN-шлюзов."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a>Пример конфигурации. Устройство Cisco ASA (IKEv2/без BGP)
Эта статья содержит пример конфигурации для устройств Cisco ASA подключение tooAzure VPN-шлюзов.

## <a name="device-at-a-glance"></a>Краткий обзор устройства

|                        |                                   |
| ---                    | ---                               |
| Поставщик устройства          | Cisco                             |
| Модель устройства           | ASA (устройство адаптивной безопасности) |
| Целевая версия         | 8.4+                              |
| Проверенная модель           | ASA 5505                          |
| Проверенные версии         | 9.2                               |
| Версия IKE            | **IKEv2**                         |
| BGP                    | **Нет**                            |
| Тип VPN-шлюза Azure | Пример VPN-шлюза **на основе маршрута**       |
|                        |                                   |

> [!NOTE]
> 1. приведенными ниже параметрами Hello подключается tooan устройств Cisco ASA Azure **на основе маршрутов** шлюза VPN с помощью настраиваемой политики IPsec/IKE с параметром «UserPolicyBasedTrafficSelectors», как описано в [в этой статье](vpn-gateway-connect-multiple-policybased-rm-ps.md).
> 2. Требуется ASA устройств toouse **IKEv2** доступа список на основе конфигурации, не VTI под управлением.
> 3. Обратитесь к спецификации поставщиков устройств VPN политики tooensure hello поддерживается на устройствах VPN локальной.

## <a name="vpn-device-requirements"></a>Требования к VPN-устройствам
Azure VPN-шлюзов с помощью стандартных IPsec/IKE туннелей S2S VPN tooestablish протокола наборов. См. слишком[сведения о VPN-устройства](vpn-gateway-about-vpn-devices.md) hello подробную параметров протокола IPsec/IKE и алгоритмов шифрования по умолчанию для VPN-шлюзы Azure. Можно дополнительно указать hello точное сочетание алгоритмов шифрования и значений длины ключа для конкретного подключения, как описано в [о требованиях к шифрования](vpn-gateway-about-compliance-crypto.md). При выборе конкретного сочетания алгоритмов шифрования и значений длины ключа убедитесь в том, что использовать соответствующие спецификации hello на устройствах VPN.

## <a name="single-vpn-tunnel"></a>Одиночный VPN-туннель
Эта топология состоит из одного VPN-туннеля S2S между VPN-шлюзом Azure и локальным устройством VPN. При необходимости можно настроить BGP через туннель VPN hello.

![Одиночный туннель](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

См. слишком[одного туннеля установки](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) подробные пошаговые инструкции toobuild hello Azure конфигураций.

### <a name="network-and-vpn-gateway-information"></a>Сведения о сети и VPN-шлюзе
В этом разделе перечислены параметры hello hello в этом примере.

| **Параметр**                | **Значение**                    |
| ---                          | ---                          |
| Префиксы адресов виртуальной сети        | 10.11.0.0/16;<br>10.12.0.0/16 |
| IP-адрес VPN-шлюза Azure         | Azure_Gateway_Public_IP      |
| Префиксы адресов в локальной среде | 10.51.0.0/16<br>10.52.0.0/16 |
| IP-адрес VPN-устройства в локальной среде    | OnPrem_Device_Public_IP     |
| *ASN для BGP виртуальной сети                | 65010                        |
| *IP-адрес узла BGP Azure           | 10.12.255.30                 |
| *ASN BGP в локальной среде         | 65050                        |
| *IP-адрес узла BGP в локальной среде     | 10.52.255.254                |
|                              |                              |

* (*) Необязательные параметры только для BGP.

### <a name="ipsecike-policy--parameters"></a>Политика и параметры IPsec/IKE

Hello перечислены hello IPsec/IKE алгоритмы и параметры, используемые в образце hello. Обратитесь к спецификации VPN устройства, toomake убедиться, что все алгоритмы, перечисленных выше поддерживаются в вашей модели устройств VPN и версии встроенного по.

| **IPsec/IKEv2**  | **Значение**                            |
| ---              | ---                                  |
| Шифрование IKEv2 | AES256                               |
| Проверка целостности IKEv2  | SHA384                               |
| Группа DH         | DHGroup24                            |
| Шифрование IPsec | AES256                               |
| Целостность IPsec  | SHA1                                 |
| Группа PFS        | PFS24                                |
| Время существования QM SA   | 7200 секунд                         |
| Селектор трафика | UsePolicyBasedTrafficSelectors $True |
| Общий ключ   | PreSharedKey                         |
|                  |                                      |

- (*) Если GCM-AES используется как алгоритм шифрования IPsec, целостность IPsec на некоторых устройствах должна быть равна NULL.

### <a name="device-notes"></a>Заметки об устройстве

>[!NOTE]
>
> 1. Для поддержки IKEv2 необходима ASA версии 8.4 и выше.
> 2. Установите ASA версии 9.x для более высокого уровня поддержки групп DH и PFS (за пределами группы 5).
> 3. Для шифрования IPsec с целостностью AES-GCM и IPsec с поддержкой SHA-256, SHA-384, SHA-512 необходимо устройство ASA версии 9.x на новом оборудовании ASA. ASA 5505, 5510, 5520, 5540, 5550 и 5580 **не** поддерживаются. (Проверьте спецификации tooconfirm hello поставщика).
>


### <a name="sample-device-configurations"></a>Примеры конфигурации устройств
Приведенный ниже сценарий Hello предоставляет образец конфигурации на основе топологии hello и параметры, приведенные выше. настройка туннеля S2S VPN Hello состоит из следующих частей hello:

1. Интерфейсы и маршруты.
2. Списки доступа.
3. Политика и параметры IKE (фаза 1 или основной режим).
4. Политика и параметры IKE (фаза 2 или быстрый режим).
5. Другие параметры (фиксация TCP MSS и т. д.).

>[!IMPORTANT] 
>Убедитесь, что завершения hello дополнительной настройки, перечисленные ниже и замените заполнители hello hello фактические значения:
> 
> - Конфигурация для внутренних и внешних интерфейсов.
> - Маршруты для внутренних (частных), внешних (общедоступных) сетей.
> - Убедитесь, все имена и номера политики должны быть уникальными в устройстве hello
> - Убедитесь, что на вашем устройстве поддерживаются алгоритмы шифрования hello
> - Замените следующие заполнителями фактическими значениями hello hello
>   - Имя внешнего интерфейса: outside;
>   - Azure_Gateway_Public_IP;
>   - OnPrem_Device_Public_IP;
>   - IKE Pre_Shared_Key;
>   - Имена виртуальной сети и шлюза локальной сети (VNetName, LNGName).
>   - Префиксы адресов виртуальной сети и локальной сети.
>   - Правильные маски сети.

#### <a name="sample-configuration"></a>Пример конфигурации

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a>Простые команды отладки

Ниже приведены некоторые команды ASA для отладки.

1. Показать hello IPsec и IKE SA
    - show crypto ipsec sa;
    - show crypto ikev2 sa.
2. Ввод режима отладки — это позволяет получить очень шумный на консоли hello
    - debug crypto ikev2 platform <level>;
    - debug crypto ikev2 protocol <level>.
3. Вывод текущих конфигураций.
    - «Показать выполнения» — отображает hello текущих конфигураций на устройстве hello; можно использовать различные подкоманды toolist определенные части конфигурации hello hello. Например, show run crypto, show run access-list, show run tunnel-group и т. д.


## <a name="next-steps"></a>Дальнейшие действия
В разделе [настройка активных VPN-шлюзов для подключений виртуальной сети для виртуальной сети и между организациями](vpn-gateway-activeactive-rm-powershell.md) действия перекрестные tooconfigure активных и подключения к виртуальной сети для виртуальной сети.

