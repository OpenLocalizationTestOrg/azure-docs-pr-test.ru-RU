---
title: "Подключение к локальной сети tooan виртуальной сети Azure: через виртуальную Частную сеть для: портал | Документы Microsoft"
description: "Действия toocreate соединении по протоколу IPsec в локальной сети tooan виртуальной сети Azure через hello общедоступный Интернет. Эти шаги помогают создавать подключения между организациями сеть-сеть VPN-шлюза, с помощью портала hello."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a>Создайте соединение сайт-сайт в hello портал Azure

В этой статье показано, как toouse hello Azure портала toocreate через виртуальную Частную сеть для подключения шлюза из вашей локальной сети toohello виртуальной сети. в этой статье инструкциям Hello применяются toohello модели развертывания диспетчера ресурсов. Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.

> [!div class="op_single_selector"]
> * [Портал Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Портал Azure (классический)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Используется tooconnect — подключение через виртуальную Частную сеть для шлюза в локальной сети tooan виртуальной сети Azure через туннель VPN IPsec/IKE (IKEv1 или IKEv2). Этот тип подключения требуется VPN устройства, расположенного в локальной среде, имеет внешний tooit открытый IP-адрес, назначенный. Дополнительные сведения о VPN-шлюзах см. в [этой статье](vpn-gateway-about-vpngateways.md).

![Схема подключения типа "сеть — сеть" через VPN-шлюз](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Перед началом работы

Убедитесь, что выполнены следующие условия перед началом настройки hello:

* Убедитесь, что у вас есть совместимых устройств VPN и тем, кто имеет доступ tooconfigure его. Дополнительные сведения о совместимых устройствах VPN и их настройке см. в [этой статье](vpn-gateway-about-vpn-devices.md).
* Убедитесь, что у вас есть общедоступный IPv4–адрес для вашего VPN–устройства. Этот IP-адрес не может располагаться вне преобразования сетевых адресов (NAT).
* Если вы не знакомы с hello диапазоны IP-адресов в вашей локальной сети, конфигурации, необходимо toocoordinate с тем, кто сможет предоставить эти сведения для вас. При создании этой конфигурации необходимо указать что Azure будет направлять в локальное расположение tooyour диапазон префиксов hello IP-адресов. Ни один из подсетей hello в локальной сети можно через Знакомство с функциями с hello подсети виртуальной сети, которые будут tooconnect для. 

### <a name="values"></a>Примеры значений

Hello примерах в этой статье используется hello следующие значения. Можно использовать эти значения toocreate тестовой среде, или ссылаться toothem toobetter понять hello примеры в этой статье.

* **Имя виртуальной сети:** TestVNet1
* **Адресное пространство:** 
  * 10.11.0.0/16;
  * 10.12.0.0/16 (необязательно для этого упражнения).
* **Подсети:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (необязательно для этого упражнения).
* **Подсеть шлюза:** 10.11.255.0/27.
* **Группа ресурсов:** TestRG1
* **Расположение:** восточная часть США.
* **DNS-сервер:** (необязательно) Hello IP-адрес DNS-сервера.
* **Имя шлюза виртуальной сети:** VNet1GW.
* **Общедоступный IP-адрес:** VNet1GWIP
* **Тип VPN:** на основе маршрутов.
* **Тип подключения:** "сеть — сеть" (IPsec)
* **Тип шлюза:** VPN.
* **Имя шлюза локальной сети:** Site2
* **Имя подключения:** VNet1toSite2

## <a name="CreatVNet"></a>1. Создать виртуальную сеть

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. Выбор DNS-сервера

DNS не требуется toocreate сайта для сайта соединением. Однако если требуется toohave разрешение имен для ресурсов, которые являются tooyour развернутой виртуальной сети, следует указать DNS-сервер. Этот параметр позволяет указать hello DNS-сервера требуется toouse для разрешения имен для этой виртуальной сети. Он не приводит к созданию DNS-сервера. См. дополнительные сведения о [разрешении имен для виртуальных машин и экземпляров ролей](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Создать подсеть шлюза hello

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Создание шлюза VPN hello

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Создание шлюза локальной сети hello

шлюз локальной сети Hello обычно относится tooyour в локальном расположении. Присвоить имя, на который Azure можно ссылаться tooit, а затем укажите hello IP-адрес сайта hello объекта toowhich устройство VPN локальной hello будет создавать подключение. Можно также указать префиксов hello IP-адресов, которые будет проходить через устройство VPN toohello шлюза VPN hello. префиксы адресов Hello, указываемые являются префиксы hello в локальной сети. Если изменения в локальной сети, или вы должны toochange hello общедоступный IP-адрес для VPN-устройства hello, можно легко обновить значения hello позже.

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. Настройка устройства VPN

Для межсайтовых подключений tooan локальной сети требуется VPN-устройства. На этом этапе мы настроим VPN-устройство. Во время настройки устройства VPN, необходимо hello следующее:

- Общий ключ. Это является hello того же самого общего ключа, указанного при создании через виртуальную Частную сеть для подключения. В наших примерах мы используем простые общие ключи. Рекомендуется создавать более сложные ключа toouse.
- Здравствуйте, общедоступный IP-адрес шлюза виртуальной сети. Hello общедоступный IP-адрес можно просмотреть с помощью hello портал Azure, PowerShell или интерфейс командной строки. hello toofind общедоступный IP-адрес шлюза VPN с помощью портала Azure hello перейдите слишком**шлюзы виртуальной сети**, затем щелкните имя hello шлюза.

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Создание VPN-подключения hello

Создайте hello сеть-сеть VPN-подключение между шлюзом виртуальной сети и локальным VPN-устройства.

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Проверьте hello VPN-подключения

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa виртуальной машины

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>Как tooreset VPN-шлюза

Сброс настроек VPN-шлюза Azure полезен при потере распределенного VPN-подключения в одном или нескольких VPN-туннелях типа "сеть-сеть". В этой ситуации локального VPN-устройств являются все работает правильно, но не удается tooestablish туннелей IPsec со шлюзами Azure VPN hello. Пошаговые инструкции см. в статье [Сброс VPN-шлюза](vpn-gateway-resetgw-classic.md).

## <a name="resize"></a>Как toochange шлюза SKU (изменение размера шлюза)

Hello шаги toochange номер SKU шлюза, см. в разделе [SKU шлюза](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="next-steps"></a>Дальнейшие действия

* Сведения о BGP см. в разделе hello [Обзор BGP](vpn-gateway-bgp-overview.md) и [как tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Сведения о принудительном туннелировании см. в статье [Настройка принудительного туннелирования с помощью классической модели развертывания](vpn-gateway-forced-tunneling-rm.md).
* Сведения о высокодоступных подключениях в режиме "активный — активный" см. в статье [Настройка высокодоступных подключений: распределенных и между виртуальными сетями](vpn-gateway-highlyavailable.md).
