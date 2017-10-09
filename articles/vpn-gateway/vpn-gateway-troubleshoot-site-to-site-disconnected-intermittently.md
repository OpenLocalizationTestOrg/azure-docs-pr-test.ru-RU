---
title: "aaaTroubleshoot VPN Azure сайт-сайт периодически отключает | Документы Microsoft"
description: "Узнайте, как tootroubleshoot hello проблемы соединений через виртуальную Частную сеть для hello регулярно отключен."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a>Устранение проблемы периодических разрывов подключений VPN типа "сеть — сеть" Azure

Могут возникнуть проблемы hello может быть нестабильным или отключает регулярно нового или существующего подключения VPN Microsoft Azure точка-сеть. В этой статье приведены Устранение toohelp действия обнаруживать и устранять hello причины проблемы hello. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Действия по устранению неполадок

### <a name="prerequisite-step"></a>Предварительные действия

Проверьте тип hello шлюза виртуальной сети Azure.

1. Go слишком[портал Azure](https://portal.azure.com).
2. Проверьте hello **Обзор** страница hello шлюз виртуальной сети для сведений о типе hello.
    
    ![Общие сведения о Hello hello шлюза](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Шаг 1 Проверьте ли hello локальной проверенных VPN-устройства

1. Узнайте, используете ли вы [проверенную версию VPN-устройства и операционной системы](vpn-gateway-about-vpn-devices.md#devicetable). Если VPN-устройства hello не проверяется, имеется toosee изготовителя устройства hello toocontact при наличии любые проблемы совместимости.
2. Убедитесь в том, что это устройство VPN hello настроен правильно. Дополнительные сведения см. на странице об [изменении примеров конфигурации устройств](vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a>Шаг 2 Проверьте hello параметры сопоставления безопасности (для шлюзов виртуальной сети Azure на основе политики)

1. Убедитесь, что hello виртуальной сети, подсети и диапазоны в hello **шлюз локальной сети** определение в Microsoft Azure, соответствуют конфигурации hello на hello локального VPN-устройства.
2. Проверьте, соответствующие параметры hello сопоставления безопасности.

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a>Шаг 3. Проверьте определяемые пользователем маршруты или группы безопасности сети в подсети шлюза

Пользовательские маршрут hello подсеть шлюза может ограничения часть трафика и разрешения других трафика. Оказывается, что hello VPN-подключения является достоверным для некоторых трафика и хорошо подходит для других. 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a>Шаг 4. Проверка Здравствуйте «один туннель VPN каждой подсети пары» (для шлюзов виртуальной сети на основе политик)

Убедитесь в том, что hello локального VPN-устройство имеет значение toohave **один туннель VPN каждой пары подсети** для шлюзов виртуальных сетей на основе политик.

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a>Шаг 5. Проверьте ограничения сопоставления безопасности (для шлюзов виртуальной сети на основе политик)

шлюз виртуальной сети на основе политик Hello ограничен 200 пар подсети сопоставления безопасности. Если количество hello подсетей виртуальной сети Azure, умноженное на время, hello число локальных подсетях больше 200, появиться случайные подсетей отключение.

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a>Шаг 6. Проверьте внешний адрес интерфейса для локального VPN-устройства

- Если hello IP-адрес устройства VPN hello в Интернете включается в hello **шлюз локальной сети** определение в Azure, могут возникать нерегулярные отключения.
- Hello внешнего интерфейса устройства должны находиться непосредственно в Интернет hello. Должно быть не сетевых адресов (NAT) или брандмауэр между hello Интернета и устройством hello.
-  При настройке брандмауэра кластеризации toohave виртуального IP-адреса, необходимо разорвать кластера hello и предоставлять hello VPN-устройством напрямую tooa открытый интерфейс, который hello шлюза может взаимодействовать с.

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a>Шаг 7 Проверка ли hello из локального VPN-устройство имеет точной пересылки (PFS) включена

Hello **точной пересылки (PFS)** функции может привести к проблемам отключения hello. Если VPN-устройства hello **точную пересылку (PFS)** включен, отключить функцию hello. Затем [обновление политики IPsec шлюза виртуальной сети hello](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).

## <a name="next-steps"></a>Дальнейшие действия

- [Настройка виртуальной сети tooa подключения сеть-сеть](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [Настройка политики IPsec/IKE для VPN-подключений типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть"](vpn-gateway-ipsecikepolicy-rm-powershell.md)

