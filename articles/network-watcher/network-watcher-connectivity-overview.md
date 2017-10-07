---
title: "Возврат tooconnectivity aaaIntroduction Наблюдатель сети Azure | Документы Microsoft"
description: "Эта страница содержит краткую hello Наблюдатель сети возможностям подключения"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a>Возврат tooconnectivity введение Наблюдатель сети Azure

Hello подключения компонент Наблюдатель сети предоставляет возможность toocheck hello прямое подключение TCP от виртуальной машины tooa виртуальной машины (VM), полное доменное имя (FQDN), URI, или IPv4-адрес. Сетевые сценарии сложные. Они реализуются с помощью групп безопасности сети, брандмауэров, определяемых пользователем маршрутов и ресурсов, предоставляемых Azure. Сложные конфигурации делают устранение неполадок, связанных с подключением, непростой задачей. Наблюдатель сети помогает уменьшить объем hello toofind времени и обнаружить проблемы с подключением. Возвращенные результаты Hello можно получить представление о ли проблема с подключением — из-за tooa платформы или неполадку конфигурации пользователя. Подключение можно проверить с помощью [PowerShell](network-watcher-connectivity-powershell.md), [Azure CLI](network-watcher-connectivity-cli.md) и [REST API](network-watcher-connectivity-rest.md).

> [!IMPORTANT]
> Для проверки возможности подключения требуется расширение виртуальной машины `AzureNetworkWatcherExtension`. Установка расширения hello на виртуальной Машине Windows на сайте [расширение виртуальной машины агента Наблюдатель сети Azure для Windows](../virtual-machines/windows/extensions-nwa.md) и виртуальной Машине Linux см. по адресу [расширение виртуальной машины агента Наблюдатель сети Azure для Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="response"></a>Ответ

Привет, в следующей таблице показаны свойства hello, возвращается, если проверка возможности подключения завершила выполнение.

|Свойство  |Описание  |
|---------|---------|
|ConnectionStatus     | состояние проверки подключения hello Hello. Возможные результаты: **Reachable** и **Unreachable**.        |
|AvgLatencyInMs     | Среднее время задержки при проверке подключения hello в миллисекундах. (Возвращается, только если подключение доступно.)        |
|MinLatencyInMs     | Проверка минимальной задержке во время подключения hello миллисекунд. (Возвращается, только если подключение доступно.)        |
|MaxLatencyInMs     | Максимальное значение задержки во время подключения hello Проверьте в миллисекундах. (Возвращается, только если подключение доступно.)        |
|ProbesSent     | Число проб, отправленных во время проверки hello. Максимальное значение — 100.        |
|ProbesFailed     | Число проб, не прошедшие проверку hello. Максимальное значение — 100.        |
|Hops     | Прыжок путем перехода из toodestination источника.        |
|Hops[].Type     | Тип ресурса. Возможные значения: **Source**, **VirtualAppliance**, **VnetLocal** и **Internet**.        |
|Hops[].Id | Уникальный идентификатор hello прыжка.|
|Hops[].Address | IP-адрес прыжка hello.|
|Hops[].ResourceId | ResourceID прыжка hello, если hello прыжка — это ресурс Azure. Если это ресурс интернета, ResourceID — это **Интернет**. |
|Hops[].NextHopIds | Hello уникальный идентификатор следующего прыжка hello выполнены.|
|Hops[].Issues | Коллекция проблемы, возникшие во время проверки hello при перехода. Если возникли проблемы отсутствуют, hello значение пусто.|
|Hops[].Issues[].Origin | В hello текущий этап, где возникла проблема. Возможные значения:<br/> **Входящий** -вызвано hello ссылку из hello предыдущих прыжка toohello текущего перехода<br/>**Исходящие** -вызвано hello ссылку из hello текущего прыжка toohello следующего прыжка<br/>**Локальный** -проблема находится на текущей прыжка hello.|
|Hops[].Issues[].Severity | Серьезность обнаруженной проблеме hello Hello. Возможные значения: **Error** и **Warning**. |
|Hops[].Issues[].Type |Тип Hello обнаружена проблема. Возможные значения: <br/>**ЦП**<br/>**Память**<br/>**GuestFirewall**<br/>**DnsResolution**<br/>**NetworkSecurityRule**<br/>**UserDefinedRoute** |
|Hops[].Issues[].Context |Сведения о обнаружена проблема hello.|
|Hops[].Issues[].Context[].key |Возвращаемый ключ из пары ключей значение hello.|
|Hops[].Issues[].Context[].value |Возвращаемое значение из пары ключей значение hello.|

Hello ниже приведен пример проблеме, обнаруженной при пересылке.

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a>Типы ошибок

Проверка возможности подключения Hello возвращает типы ошибку о подключении hello. Hello следующей таблице приведен список типов hello текущей ошибки возвращаются.

|Тип  |Описание  |
|---------|---------|
|ЦП     | Высокая загрузка ЦП.       |
|Память     | Высокий уровень использования памяти.       |
|GuestFirewall     | Трафик блокируется из-за конфигурации брандмауэра tooa виртуальной машины.        |
|DnsResolution     | Сбой разрешения DNS для адреса назначения hello.        |
|NetworkSecurityRule    | Трафик блокируется правилом группы безопасности сети (возвращается правило).        |
|UserDefinedRoute|Трафик удаляется из-за определенные пользователем tooa или маршрут системы. |

### <a name="next-steps"></a>Дальнейшие действия

Узнайте, как ресурс tooa подключения к tooverify, посетив: [проверки связи с Наблюдатель сети Azure](network-watcher-connectivity-powershell.md).

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

