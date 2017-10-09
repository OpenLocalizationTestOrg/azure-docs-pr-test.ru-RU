---
title: "aaaDiagnose локальные подключения через шлюз VPN с Наблюдатель сети Azure | Документы Microsoft"
description: "В этой статье описывается, как toodiagnose локального подключения через VPN-шлюза в устранении неполадок ресурса Наблюдатель сети Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9941c5d1b49bec29062210684dae8653cbdb84b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-on-premises-connectivity-via-vpn-gateways"></a>Диагностика локальных подключений через VPN-шлюзы

Шлюз VPN Azure позволяет toocreate гибридное решение, для устранения необходимости hello безопасного соединения между локальной сетью и виртуальной сети Azure. Как требования к уникальным, поэтому — выбор hello локального устройства VPN. В настоящее время Azure поддерживает [несколько VPN-устройства](../vpn-gateway/vpn-gateway-about-vpn-devices.md#devicetable) , которые постоянно проверяются в условиях партнерства поставщиков устройств hello. Просмотрите параметры конфигурации конкретного устройства hello перед началом настройки локальных VPN-устройства. VPN-шлюз Azure настраивается с помощью набора [поддерживаемых параметров IPsec](../vpn-gateway/vpn-gateway-about-vpn-devices.md#ipsec), которые используются для установления подключений. В настоящее время нет возможности для вас toospecify или выбрать определенное сочетание параметров IPsec из hello шлюза VPN Azure. Для успешного соединения между локальной средой и Azure, hello локальные параметры VPN-устройства должен быть в соответствии с параметры IPsec hello, указанный в параметре шлюза VPN Azure. Если hello следующие значения в правильный, потере подключения и до сих пор устранении этих проблем не тривиальный, обычно заняла часов tooidentify и исправьте проблему hello.

С hello Наблюдатель сети Azure устранения неполадок компонентов, вы могли toodiagnose проблемах, связанных с шлюзом и подключения и в течение минут имеют достаточно toomake сведения toorectify hello обоснованное решение проблемы.

## <a name="scenario"></a>Сценарий

Вы хотите tooconfigure сайта для сайта подключение между Azure и локальной с помощью FortiGate как hello локального шлюза VPN. tooachieve этом случае требуется hello, после завершения программы установки:

1. Шлюз виртуальной сети - hello VPN-шлюза в Azure
1. Шлюз локальной сети — hello [локального шлюза VPN (FortiGate)](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) представление в облаке Azure
1. Сайт сайт подключения (на основе политики) - [соединение между hello шлюза VPN и hello локального маршрутизатора](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#createconnection)
1. [Configuring FortiGate](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/Site-to-Site_VPN_using_FortiGate.md) (Настройка FortiGate)

Подробные пошаговые инструкции по настройке конфигурации сайта для сайта можно найти по следующему адресу: [создать виртуальную сеть с подключением сайт-сайт с помощью портала Azure hello](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

Одно из действий важной hello настраивающий параметры подключения IPsec hello, любые ошибки в конфигурации приводит tooloss подключения между hello локальной сетью и Azure. В настоящее время VPN-шлюзы Azure, настроенным toosupport hello следующие параметры IPsec на этапе 1. Обратите внимание, что, как упоминалось ранее, эти параметры нельзя изменить.  Как видно в следующей таблице hello hello алгоритмы шифрования, поддерживаемые шлюзом VPN Azure, AES256 и AES128, 3DES.

### <a name="ike-phase-1-setup"></a>Этап 1 настройки протокола IKE

| **Свойство** | **PolicyBased** | **Стандартный или высокопроизводительный VPN-шлюз с маршрутизацией на основе маршрутов** |
| --- | --- | --- |
| Версия IKE |IKEv1 |IKEv2 |
| Группа Диффи — Хелмана |Группа 2 (1024 бита) |Группа 2 (1024 бита) |
| Метод проверки подлинности |Общий ключ |Общий ключ |
| Алгоритмы шифрования |AES256 AES128 3DES |AES256 3DES |
| Алгоритм хэширования |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| Время существования сопоставления безопасности первого этапа (время) |28 800 сек |10 800 секунд |

Как пользователь, будет необходимо tooconfigure вашей FortiGate приведен пример конфигурации можно найти на [GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/fortigate_show%20full-configuration.txt). Непреднамеренно вашей FortiGate toouse SHA-512 настроен в качестве хэш-алгоритм hello. Так как этот алгоритм не поддерживается для подключений на основе политик, VPN-подключение не будет работать.

Эти вопросы, жестких tootroubleshoot и основных причин часто неочевидным. В этом случае можно открыть справки билет tooget по устранению проблемы hello. Но с помощью API устранения неполадок Наблюдателя за сетями Azure вы сможете выявлять эти проблемы самостоятельно.

## <a name="troubleshooting-using-azure-network-watcher"></a>Устранение неполадок с помощью Наблюдателя за сетями Azure

toodiagnose подключение, подключение tooAzure PowerShell и инициировать hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` командлета. Hello сведения об использовании этого командлета в [Устранение неполадок шлюза виртуальной сети и подключения - PowerShell](network-watcher-troubleshoot-manage-powershell.md). Этот командлет может занять до минуты toocomplete toofew.

Можно перемещаться по завершении командлета hello toohello место хранения, указанной в командлет hello tooget подробные сведения на о проблеме hello и журналы. Azure Наблюдатель сети создает ZIP-папки, содержащей hello следующие файлы журнала:

![1][1]

Привет открыть файл с именем IKEErrors.txt и он отображает hello следующие ошибки, указывает на проблему с локальными неправильной настройки параметра IKE.

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

Подробные сведения можно получить из hello Scrubbed wfpdiag.txt об ошибке hello, как в этом случае сообщение о том, что было `ERROR_IPSEC_IKE_POLICY_MATCH` , tooconnection интерес, не работает должным образом.

Другой распространенная ошибка — hello, указав неверный общие ключи. В случае hello предшествующий примере выбраны различные общие ключи, hello IKEErrors.txt показывает hello следующая ошибка: `Error: Authentication failed. Check shared key`.

Функция, устранение неполадок Azure Наблюдатель сети позволяет toodiagnose и устранения неполадок шлюза VPN и подключение с легкостью hello простого командлета PowerShell. В настоящее время мы поддержки диагностики hello, следующие условия и работаем над Добавление дополнительные условия.

### <a name="gateway"></a>Шлюз

| Тип ошибки | Причина | Журнал|
|---|---|---|
| NoFault | Ошибка не обнаружена. |Да|
| GatewayNotFound | Не удается найти шлюз или шлюз не подготовлен. |Нет|
| PlannedMaintenance |  Выполняется обслуживание экземпляра шлюза.  |Нет|
| UserDrivenUpdate | Идет обновление, инициированное пользователем. Это может быть операция изменения размера. | Нет |
| VipUnResponsive | Не удается связаться с hello первичного экземпляра hello шлюза. Это происходит, когда происходит сбой проверки работоспособности hello. | Нет |
| PlatformInActive | Имеется проблема с платформой hello. | Нет|
| ServiceNotRunning | базовая служба Hello не выполняется. | Нет|
| NoConnectionsFoundForGateway | Подключения не существует в шлюзе hello. Это всего лишь предупреждение.| Нет|
| ConnectionsNotConnected | Ни одно из подключений hello связаны. Это всего лишь предупреждение.| Да|
| GatewayCPUUsageExceeded | текущее использование шлюза Hello ЦП — > 95%. | Да |

### <a name="connection"></a>Подключение

| Тип ошибки | Причина | Журнал|
|---|---|---|
| NoFault | Ошибка не обнаружена. |Да|
| GatewayNotFound | Не удается найти шлюз или шлюз не подготовлен. |Нет|
| PlannedMaintenance | Выполняется обслуживание экземпляра шлюза.  |Нет|
| UserDrivenUpdate | Идет обновление, инициированное пользователем. Это может быть операция изменения размера.  | Нет |
| VipUnResponsive | Не удается связаться с hello первичного экземпляра hello шлюза. Это происходит, когда происходит сбой проверки работоспособности hello. | Нет |
| ConnectionEntityNotFound | Отсутствует конфигурация подключения. | Нет |
| ConnectionIsMarkedDisconnected | Hello подключения помечен «отключенной». |Нет|
| ConnectionNotConfiguredOnGateway | Hello базовой службы не имеет настроенного подключения hello. | Да |
| ConnectionMarkedStandy | соответствующая служба Hello помечается как standby.| Да|
| Аутентификация | Несоответствие предварительного ключа. | Да|
| PeerReachability | Hello одноранговых шлюз недоступен. | Да|
| IkePolicyMismatch | Hello одноранговых шлюза имеет IKE политики, которые не поддерживаются в Azure. | Да|
| WfpParse Error | Ошибка синтаксического анализа журнала WFP hello. |Да|

## <a name="next-steps"></a>Дальнейшие действия

Узнайте toocheck подключения шлюза VPN с помощью PowerShell и автоматизации Azure, посетив [шлюзах VPN монитор с устранением неполадок Наблюдатель сети Azure](network-watcher-monitor-with-azure-automation.md)

[1]: ./media/network-watcher-diagnose-on-premises-connectivity/figure1.png
