---
title: "на основе aaaURL содержимого Общие сведения о маршрутизации | Документы Microsoft"
description: "Эта страница Обзор hello URL-адрес шлюза приложения-маршрутизация на основе содержимого, конфигурации UrlPathMap и PathBasedRouting правило."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: 4409159b-e22d-4c9a-a103-f5d32465d163
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: gwallace
ms.openlocfilehash: 5094b42625baffeb395beace68db0d269e46080c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="url-path-based-routing-overview"></a>Общие сведения о маршрутизации на основе URL-путей

URL-адрес на основе маршрутизации путей позволяет вам tooroute трафика tooback окончания пулов серверов на основании путей к URL-адрес запроса hello. 

Одним из сценариев hello является tooroute запросов для различных типов содержимого toodifferent внутреннего сервера пулов.

В следующем примере hello, шлюз приложений обслуживающий трафик для contoso.com из трех серверных пулов например: VideoServerPool, ImageServerPool и DefaultServerPool.

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

Запросы для http://contoso.com/video * перенаправленное tooVideoServerPool, и http://contoso.com/images * это перенаправленное tooImageServerPool. DefaultServerPool выбирается в том случае, если ни один из шаблонов путей hello соответствует.

> [!IMPORTANT]
> Правила обрабатываются в порядке hello, в котором они перечислены в портале hello. Это весьма рекомендуемые к использованию tooconfigure несколькими сайтами прослушивателей первый предыдущего tooconfiguring основные прослушивателя.  Это гарантирует завершение этого трафика получает перенаправленное toohello самому началу. Если базовый прослушиватель стоит первым в списке и совпадает с входящим запросом, он будет обрабатываться прослушивателем.

## <a name="urlpathmap-configuration-element"></a>Элемент конфигурации UrlPathMap

элемент urlPathMap Hello — сопоставления пула серверов используется toospecify путь шаблоны tooback-end. Hello следующий пример кода представляет фрагмент кода hello urlPathMap элемента из файла шаблона.

```json
"urlPathMaps": [{
    "name": "{urlpathMapName}",
    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/urlPathMaps/{urlpathMapName}",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/    {subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName1}"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpSettingsList/{settingname1}"
        },
        "pathRules": [{
            "name": "{pathRuleName}",
            "properties": {
                "paths": [
                    "{pathPattern}"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName2}"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpsettingsList/{settingName2}"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> PathPattern: Этот параметр является списком toomatch шаблонов пути. Каждый должно начинаться с / и hello единственное место «*» разрешается в hello окончания следовать «/». Строка Hello переданы сопоставителе toohello путь не содержит текст после hello сначала? или # и эти символы не допускаются.

Дополнительные сведения см. в статье [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) (Шаблон Resource Manager с использованием маршрутизации на основе URL-адресов).

## <a name="pathbasedrouting-rule"></a>Правило PathBasedRouting

RequestRoutingRule типа PathBasedRouting — используется toobind urlPathMap tooa прослушивателя. Все получаемые запросы для этого прослушивателя распределяются согласно политике, указанной в urlPathMap.
Фрагмент правила PathBasedRouting:

```json
"requestRoutingRules": [
    {

"name": "{ruleName}",
"id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/requestRoutingRules/{ruleName}",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/ urlPathMaps/{urlpathMapName}"
    },

}
    }
]
```

## <a name="next-steps"></a>Дальнейшие действия

После изучения маршрутизации содержимого на основе URL-адрес, go слишком[создать с помощью маршрутизации на основе URL-адрес шлюза приложения](application-gateway-create-url-route-portal.md) toocreate шлюза с правилами маршрутизации URL-адрес приложения.
