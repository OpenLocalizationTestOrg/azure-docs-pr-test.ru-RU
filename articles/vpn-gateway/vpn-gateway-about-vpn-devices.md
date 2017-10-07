---
title: "aaaAbout VPN-устройства для соединения с Azure между организациями | Документы Microsoft"
description: "В этой статье описываются VPN-устройства и параметры IPsec для подключений типа \"сеть — сеть\" через VPN-шлюз, Здесь представлены ссылки, tooconfiguration инструкции и примеры."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: ba449333-2716-4b7f-9889-ecc521e4d616
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: yushwang;cherylmc
ms.openlocfilehash: 8b84afbf93d807342ecd56ab369d5909a13343e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>VPN-устройства и параметры IPsec/IKE для подключений типа "сеть — сеть" через VPN-шлюз

VPN-устройство является обязательным tooconfigure VPN-подключения между организациями сайтами (S2S) с помощью шлюза VPN. Для межсайтовых подключений можно используется toocreate гибридное решение, или при необходимости безопасных соединений между вашей локальной сети и виртуальные сети. В этой статье перечислены проверенные VPN-устройства и параметры IPsec/IKE для VPN-шлюзов.

> [!IMPORTANT]
> При возникновении проблем с подключением между локальными устройствами VPN и шлюзах VPN см. слишком[известные проблемы совместимости устройства](#known).
>
>

### <a name="items-toonote-when-viewing-hello-tables"></a>Элементы toonote при просмотре таблицы hello:

* Изменилась терминология, связанная с VPN-шлюзами Azure. Только имена hello были изменены. Функциональность осталась прежней,
  * Статическая маршрутизация — на основе политик (PolicyBased).
  * Динамическая маршрутизация — на основе маршрутов (RouteBased).
* Спецификации для шлюза VPN высокопроизводительные и routebased VPN-шлюза hello же, если не указано иное. Например проверка hello VPN-устройства, совместимые со шлюзами VPN routebased совместимы с hello высокопроизводительные VPN-шлюз.

## <a name="devicetable"></a>Проверенные VPN-устройства и руководства по конфигурации устройства

> [!NOTE]
> При настройке подключения типа "сеть — сеть" для VPN-устройства необходимо указывать общедоступный IP-адрес IPv4.
>

В сотрудничестве с поставщиками устройств мы утвердили набор стандартных VPN-устройств. Все устройства hello в семействах устройств hello в hello после списка должна работать со шлюзами VPN. В разделе [о параметры шлюза VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype) toounderstand hello VPN введите используйте hello решения VPN-шлюза необходимо tooconfigure (PolicyBased или routebased.).

toohelp настроить устройство VPN см. в соответствующих семейства устройств tooappropriate toohello связей. Hello ссылки tooconfiguration инструкции на наилучшим возможным образом. За поддержкой VPN-устройства обратитесь к его изготовителю.

|**поставщик**          |**Семейство устройств**     |**Минимальная версия ОС** |**Инструкции по настройке PolicyBased** |**Инструкции по настройке RouteBased** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |Не совместимо  |[Руководство по настройке](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |VPN-маршрутизаторы серии AR |2.9.2                  |Скоро     |Не совместимо  |
| Barracuda Networks, Inc. |Брандмауэр Barracuda NextGen серии F |PolicyBased: 5.4.3<br>RouteBased: 6.2.0 |[Руководство по настройке](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[Руководство по настройке](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Брандмауэр Barracuda NextGen серии Х |Barracuda Firewall 6.5 |[Руководство по настройке](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |Не совместимо |
| Brocade            |Vyatta 5400 vRouter   |Virtual Router 6.6R3 GA|[Руководство по настройке](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |Не совместимо |
| Check Point |Security Gateway |R77.30 |[Руководство по настройке](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[Руководство по настройке](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco              |ASA       |8.3 |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |Не совместимо |
| Cisco |ASR |PolicyBased: IOS 15.1<br>RouteBased: IOS 15.2 |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |PolicyBased: IOS 15.0<br>RouteBased*: IOS 15.1 |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[Примеры настройки*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX, SDX, VPX |10.1 и выше |[Руководство по настройке](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |Не совместимо |
| F5 |Серия BIG-IP |12.0 |[Руководство по настройке](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[Руководство по настройке](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.4.2 |  |[Руководство по настройке](http://cookbook.fortinet.com/ipsec-vpn-microsoft-azure-54) |
| Internet Initiative Japan (IIJ) |Серия SEIL |SEIL/X 4.60<br>SEIL/B1 4.60<br>SEIL/x86 3.20 |[Руководство по настройке](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |Не совместимо |
| Juniper |SRX |PolicyBased: JunOS 10.2<br>Routebased: JunOS 11.4 |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |Серия J |PolicyBased: JunOS 10.4r9<br>RouteBased: JunOS 11.4 |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[Примеры конфигурации](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |Служба маршрутизации и удаленного доступа |Windows Server 2012 |Не совместимо |[Примеры конфигурации](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| Open Systems AG |Шлюз безопасности Mission Control |Недоступно |[Руководство по настройке](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |Не совместимо |
| Openswan |Openswan |2.6.32 |(Ожидается в ближайшее время) |Не совместимо |
| Palo Alto Networks |Все устройства под управлением PAN-OS |PAN-OS<br>PolicyBased: 6.1.5 или более поздней версии<br>RouteBased: 7.1.4 |[Руководство по настройке](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[Руководство по настройке](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWall |Серия TZ и NSA<br>Серия SuperMassive<br>Серия NSA класса E |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |[Configuration guide for SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646) (Руководство по настройке SonicOS 6.2)<br>[Configuration guide for SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) (Руководство по настройке SonicOS 5.9) |[Configuration guide for SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646) (Руководство по настройке SonicOS 6.2)<br>[Configuration guide for SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) (Руководство по настройке SonicOS 5.9) |
| WatchGuard |Все |Fireware XTM<br> PolicyBased: 11.11.x<br>RouteBased: 11.12.x |[Руководство по настройке](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[Руководство по настройке](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

* Маршрутизаторы ISR серии 7200 поддерживают только VPN типа PolicyBased.

## <a name="additionaldevices"></a>Непроверенные VPN-устройства

Если вы не видите устройства, перечисленные в таблице устройств VPN проверки hello, устройства по-прежнему могут работать с подключением сайт-сайт. Чтобы получить дополнительную информацию и инструкции по настройке, обратитесь к изготовителю устройства.

## <a name="editing"></a>Изменение примеров конфигурации устройств

После загрузки образец конфигурации устройства VPN hello предоставлен вам потребуется tooreplace некоторые hello значения tooreflect hello параметры среды.

### <a name="tooedit-a-sample"></a>tooedit пример:

1. Откройте образец hello, с помощью блокнота.
2. Поиск и замена всех <*текст*> строки со значениями hello, относятся tooyour среды. Быть убедиться, что tooinclude < и >. Если указано имя hello имя должно быть уникальным. Если команда не работает, обратитесь к документации изготовителя устройства.

| **Пример текста** | **Изменить на** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |Выбранное имя для данного объекта. Пример: myOnPremisesNetwork. |
| &lt;RP_AzureNetwork&gt; |Выбранное имя для данного объекта. Пример: myAzureNetwork. |
| &lt;RP_AccessList&gt; |Выбранное имя для данного объекта. Пример: myAzureAccessList. |
| &lt;RP_IPSecTransformSet&gt; |Выбранное имя для данного объекта. Пример: myIPSecTransformSet. |
| &lt;RP_IPSecCryptoMap&gt; |Выбранное имя для данного объекта. Пример: myIPSecCryptoMap. |
| &lt;SP_AzureNetworkIpRange&gt; |Укажите диапазон. Пример: 192.168.0.0. |
| &lt;SP_AzureNetworkSubnetMask&gt; |Укажите маску подсети. Пример: 255.255.0.0. |
| &lt;SP_AzureNetworkIpRange&gt; |Укажите локальный диапазон. Пример: 10.2.1.0. |
| &lt;SP_AzureNetworkSubnetMask&gt; |Укажите локальную маску подсети. Пример: 255.255.255.0. |
| &lt;SP_AzureGatewayIpAddress&gt; |Эта виртуальная сеть tooyour определенные сведения и расположен в hello портал управления как **IP-адрес шлюза**. |
| &lt;SP_PresharedKey&gt; |Эти сведения конкретного tooyour виртуальной сети и находится в hello портал управления как управление ключами. |

## <a name="ipsec"></a>Параметры IPsec/IKE

> [!NOTE]
> Несмотря на то, что hello значения, перечисленные в следующей таблице hello поддерживаются hello VPN-шлюза, в настоящее время существует отсутствует механизм toospecify или выберите определенное сочетание алгоритмов или параметров из шлюза VPN hello. Необходимо указать все ограничения из hello локального VPN-устройства. Кроме того, необходимо установить для **MSS** значение **1350**.
> 
>

В hello следующие таблицы:

* SA — сопоставление безопасности.
* Этап 1 IKE также называется "Главный режим".
* Этап 2 IKE также называется "Быстрый режим".

### <a name="ike-phase-1-main-mode-parameters"></a>Параметры этапа 1 IKE (главный режим)

| **Свойство**          |**PolicyBased**    | **RouteBased**    |
| ---                   | ---               | ---               |
| Версия IKE           |IKEv1              |IKEv2              |
| Группа Диффи — Хелмана  |Группа 2 (1024 бита) |Группа 2 (1024 бита) |
| Метод проверки подлинности |Общий ключ     |Общий ключ     |
| Алгоритмы шифрования и хэширования |1. AES256, SHA256<br>2) AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |1. AES256, SHA1<br>2) AES256, SHA256<br>3. AES128, SHA1<br>4. AES128, SHA256<br>5. 3DES, SHA1<br>6. 3DES, SHA256 |
| Срок действия SA           |28 800 сек     |28 800 сек     |

### <a name="ike-phase-2-quick-mode-parameters"></a>Параметры этапа 2 IKE (быстрый режим)

| **Свойство**                  |**PolicyBased**| **RouteBased**                              |
| ---                           | ---           | ---                                         |
| Версия IKE                   |IKEv1          |IKEv2                                        |
| Алгоритмы шифрования и хэширования |1. AES256, SHA256<br>2) AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |[Предложения по сопоставлению безопасности в быстром режиме на основе маршрутизации](#RouteBasedOffers) |
| Срок действия SA (время)            |3600 секунд  |27 000 секунд                                |
| Срок действия SA (байты)           |102 400 000 КБ | -                                           |
| Полная безопасность пересылки (PFS) |Нет             |[Предложения по сопоставлению безопасности в быстром режиме на основе маршрутизации](#RouteBasedOffers) |
| Обнаружение неиспользуемых одноранговых узлов (DPD)     |Не поддерживается  |Поддерживаются                                    |


### <a name ="RouteBasedOffers"></a>Предложения по сопоставлению безопасности IPsec для VPN на основе маршрутов (в быстром режиме)

Hello следующей таблице перечислены предложения IPsec SA (быстрый режим IKE). Предложения, перечисленных hello порядок предпочтения представления или принятия предложения, hello.

#### <a name="azure-gateway-as-initiator"></a>Шлюз Azure в качестве инициатора

|-  |**Шифрование**|**Аутентификация**|**Группа PFS**|
|---| ---          |---               |---          |
| 1 |GCM AES256    |GCM (AES256)      |None         |
| 2 |AES256        |SHA1              |None         |
| 3 |3DES          |SHA1              |None         |
| 4 |AES256        |SHA256            |None         |
| 5 |AES128        |SHA1              |None         |
| 6 |3DES          |SHA256            |None         |

#### <a name="azure-gateway-as-responder"></a>Шлюз Azure в качестве ответчика

|-  |**Шифрование**|**Аутентификация**|**Группа PFS**|
|---| ---          | ---              |---          |
| 1 |GCM AES256    |GCM (AES256)      |None         |
| 2 |AES256        |SHA1              |None         |
| 3 |3DES          |SHA1              |None         |
| 4 |AES256        |SHA256            |None         |
| 5 |AES128        |SHA1              |None         |
| 6 |3DES          |SHA256            |None         |
| 7 |DES           |SHA1              |None         |
| 8 |AES256        |SHA1              |1            |
| 9 |AES256        |SHA1              |2            |
| 10|AES256        |SHA1              |14           |
| 11|AES128        |SHA1              |1            |
| 12|AES128        |SHA1              |2            |
| 13.|AES128        |SHA1              |14           |
| 14|3DES          |SHA1              |1            |
| 15|3DES          |SHA1              |2            |
| 16|3DES          |SHA256            |2            |
| 17|AES256        |SHA256            |1            |
| 18|AES256        |SHA256            |2            |
| 19|AES256        |SHA256            |14           |
| 20|AES256        |SHA1              |24           |
| 21|AES256        |SHA256            |24           |
| 22|AES128        |SHA256            |None         |
| 23|AES128        |SHA256            |1            |
| 24|AES128        |SHA256            |2            |
| 25|AES128        |SHA256            |14           |
| 26|3DES          |SHA1              |14           |

* Вы можете указать NULL-шифрование ESP IPsec для высокопроизводительных VPN-шлюзов и VPN-шлюзов типа RouteBased. Значение NULL на основе шифрование не обеспечивает защиты toodata во время передачи и должен использоваться только при максимальной пропускной способности и минимальной задержки является обязательным. Клиенты могут выбрать toouse это в сценарии взаимодействия виртуальной сети для виртуальной сети или шифрования применяется в другом месте в решении hello.
* Для подключений между организациями через Интернет hello используйте параметры шлюза Azure VPN по умолчанию hello с алгоритмами шифрования и хэширования перечислены в таблицах hello выше tooensure безопасности важных взаимодействий.

## <a name="known"></a>Известные проблемы совместимости устройств

> [!IMPORTANT]
> Они являются hello известные проблемы совместимости между сторонних VPN-устройствах и шлюзах Azure VPN. Hello команды Azure активно сотрудничает с поставщиками hello tooaddress hello перечисленных ниже проблем. После разрешения проблемы hello, эта страница будет обновляться hello наиболее актуальные сведения. Рекомендуется периодически просматривать ее.
>
>

### <a name="feb-16-2017"></a>16 февраля 2017 г.

**Компьютер Пало сетей устройствами с помощью too7.1.4 предыдущие версии** для Azure VPN на основе маршрутов: Если с помощью VPN-устройства от сети компьютер Пало too7.1.4 предыдущие версии PAN-OS и возникают подключения выдает tooAzure шлюзах VPN на основе маршрутов выполните следующие шаги hello.

1. Проверьте версию встроенного по hello устройства Пало компьютер сети. Если вашей PAN-OS версии более ранней, чем 7.1.4, обновите too7.1.4.
2. На устройстве hello Пало компьютер сети, измените too28 время существования по hello SA Фаза 2 (или SA быстрого режима), 800 секунд (8 часов) при подключении toohello VPN-шлюз Azure.
3. Если по-прежнему возникают проблемы с подключением, откройте запрос на техническую поддержку от hello портал Azure.
