---
title: "aaaMonitor операции, события и счетчики для Nsg | Документы Microsoft"
description: "Узнайте, как tooenable счетчики, события и оперативной ведение журнала для Nsg"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a>Аналитика журналов для групп безопасности сети

Можно включить следующие категории журнала диагностики для Nsg hello:

* **Событие:** содержит записи, для какой NSG правила, примененных tooVMs и экземпляр роли, на основе MAC-адреса. Сбор сведений о состоянии Hello для этих правил каждые 60 секунд.
* **Счетчик правил:** содержит записи для сколько раз каждый NSG правило будет применяться toodeny или разрешить трафик.

> [!NOTE]
> Журналы диагностики доступны только для Nsg, развернутые с помощью модели развертывания диспетчера ресурсов Azure hello. Невозможно включить сбор данных диагностики для Nsg, развернутые с помощью hello классической модели развертывания. Для лучшего понимания hello двух моделей, ссылаются на hello [Azure основные сведения о моделях развертывания](../resource-manager-deployment-model.md) статьи.

Ведение журнала действий (ранее он назывался журналом аудита или рабочим журналом) включена по умолчанию для всех NSG, независимо от модели развертывания. toodetermine операции, которые были выполнены на Nsg в журнале активности hello, найдите записи, содержащие hello следующие типы ресурсов: 

- Microsoft.ClassicNetwork/networkSecurityGroups 
- Microsoft.ClassicNetwork/networkSecurityGroups/securityRules
- Microsoft.Network/networkSecurityGroups
- Microsoft.Network/networkSecurityGroups/securityRules 

Чтение hello [Обзор hello журнал действий Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) toolearn статьи, Дополнительные сведения о журналах активности. 

## <a name="enable-diagnostic-logging"></a>Включение ведения журналов диагностики

Необходимо включить ведение журнала диагностики для *каждого* NSG требуется toocollect данные. Hello [Обзор служб Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) статье объясняется, где можно отправить журналы диагностики. При отсутствии существующей NSG hello завершения шагов в hello [создайте группу безопасности сети](virtual-networks-create-nsg-arm-pportal.md) toocreate статье один. Можно включить NSG ведения журналов с помощью любого из следующих методов hello диагностики:

### <a name="azure-portal"></a>Портал Azure

Ведение журнала портала tooenable hello toouse, toohello входа [портала](https://portal.azure.com). Щелкните **дополнительные службы**, затем введите *группы безопасности сети*. Выберите hello требуется ведение журнала для tooenable NSG. Следуйте инструкциям hello не вычислительные ресурсы на hello [включить журналы диагностики в портале hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) статьи. Выберите категории журналов: **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter** или обе сразу.

### <a name="powershell"></a>PowerShell

tooenable PowerShell toouse ведения журнала, выполните инструкции hello hello [включить журналы диагностики с помощью PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) статьи. Оцените следующие сведения перед вводом команды из статьи hello hello.

- Можно определить toouse значение hello для hello `-ResourceId` параметра, заменив hello после [текст] соответствующим образом, введя команду hello `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`. выходные данные идентификатор Hello hello команды выглядят примерно слишком*/subscriptions/ [имя подписки Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Toocollect данных из категории журнала требуется только добавить `-Categories [category]` toohello конец команды hello в статье hello, где категории равна *NetworkSecurityGroupEvent* или *NetworkSecurityGroupRuleCounter*. Если вы не используете hello `-Categories` параметра, сбор данных включен для обоих журналов категорий.

### <a name="azure-command-line-interface-cli"></a>интерфейс командной строки Azure (CLI)

toouse Здравствуйте ведения журнала tooenable CLI, следуйте инструкциям hello hello [включить журналы диагностики через CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) статьи. Оцените следующие сведения перед вводом команды из статьи hello hello.

- Можно определить toouse значение hello для hello `-ResourceId` параметра, заменив hello после [текст] соответствующим образом, введя команду hello `azure network nsg show [resource-group-name] [nsg-name]`. выходные данные идентификатор Hello hello команды выглядят примерно слишком*/subscriptions/ [имя подписки Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Toocollect данных из категории журнала требуется только добавить `-Categories [category]` toohello конец команды hello в статье hello, где категории равна *NetworkSecurityGroupEvent* или *NetworkSecurityGroupRuleCounter*. Если вы не используете hello `-Categories` параметра, сбор данных включен для обоих журналов категорий.

## <a name="logged-data"></a>Собранные данные журнала

Данные в оба журнала записываются в формате JSON. в следующих разделах hello указывается Hello определенные данные, записанные для каждого типа журнала.

### <a name="event-log"></a>Журнал событий
Этот журнал содержит сведения о NSG, какие правила применяются tooVMs и облачной службы экземпляры роли, на основе MAC-адреса. Следующий пример данных Hello регистрируется для каждого события.

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a>Журнал счетчиков правил

Этот журнал содержит сведения о каждом tooresources правило применяется. Hello следующий пример данных регистрируется каждый раз, когда применяется правило.

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a>Просмотр и анализ журналов

toolearn tooview действия записываются в журнал, чтение hello [Обзор hello журнал действий Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) статьи. toolearn tooview диагностики ведения журнала данных, чтение hello [Обзор служб Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) статьи. При отправке данных диагностики tooLog Analytics, можно использовать hello [сетевой группы безопасности Azure analytics](../log-analytics/log-analytics-azure-networking-analytics.md) решение для управления (Предварительная версия) для расширенного анализа. 
