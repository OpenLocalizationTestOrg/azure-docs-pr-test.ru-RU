---
title: "Поддержка aaaWebSocket в шлюз приложений Azure | Документы Microsoft"
description: "Эта страница Обзор hello поддержка WebSocket шлюза приложения."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: amsriva
ms.openlocfilehash: 3776117803e8559ad243c2d4c3dd661199c1e48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a>Общие сведения о поддержке WebSocket в шлюзе приложений

Шлюз приложений обеспечивает встроенную поддержку WebSocket независимо от размера. Нет пользовательских параметр tooselectively enable или disable поддержка WebSocket. 

Протокол WebSocket, стандартизированный в [RFC6455](https://tools.ietf.org/html/rfc6455), обеспечивает полнодуплексную связь между сервером и клиентом через длительное TCP-подключение. Эта функция обеспечивает более интерактивного взаимодействия между hello веб-сервера и клиента hello, которое может быть двунаправленной без необходимости hello опроса, как требуется в реализации на основе HTTP. WebSocket имеет минимальные издержки в отличие от HTTP, и можно повторно использовать hello же TCP-подключение для нескольких запросов/ответов приведет к более эффективное использование ресурсов. Протоколы WebSocket спроектированный toowork превышают традиционных HTTP-порты 80 и 443.

Можно продолжить, используя стандартный прослушиватель HTTP на порт 80 или 443 tooreceive WebSocket трафика. Трафик WebSocket —, направленной toohello WebSocket включается внутреннему серверу с помощью hello соответствующие внутреннего пула, как указано в правилах шлюз приложений. Hello внутренний сервер должен отвечать зонды шлюза toohello приложения, которые описаны в hello [обзор проверки работоспособности](application-gateway-probe-overview.md) раздела. Проверки работоспособности шлюза приложений выполняются только по протоколам HTTP или HTTPS. Каждого сервера базы данных, должен отвечать tooHTTP зонды для приложения tooroute WebSocket трафика toohello шлюза.

## <a name="listener-configuration-element"></a>Элемент конфигурации прослушивателя

Существующего прослушивателя HTTP можно использовать toosupport трафика WebSocket. Hello ниже приведен фрагмент HTTP-прослушивателей элемента из образец файла шаблона. Вам потребуется требуется прослушивателей HTTP и HTTPS, toosupport WebSocket и защита трафика WebSocket. Аналогично можно использовать hello [портала](application-gateway-create-gateway-portal.md) или [PowerShell](application-gateway-create-gateway-arm.md) toocreate шлюза приложения с прослушивателями на порт 80 или 443 toosupport WebSocket трафик.

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/DefaultFrontendPublicIP"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort443'"
                },
                "Protocol": "Https",
                "SslCertificate": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/sslCertificates/appGatewaySslCert1'"
                },
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a>BackendAddressPool, BackendHttpSetting и конфигурация правила маршрутизации

BackendAddressPool — используется toodefine внутренний пул с серверами WebSocket включены. Hello backendHttpSetting определена внутренний порт 80 и 443. свойства Hello сопоставление на основе файлов cookie и requestTimeouts не применимо tooWebSocket трафика. Нет изменений в правила маршрутизации hello, «Basic» используется tootie hello соответствующего прослушивателя toohello соответствующий серверный пул адресов. 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a>Сервер с поддержкой WebSocket

Серверной части должен иметь HTTP/HTTPS веб-сервер на hello настроен порт (обычно 80 или 443) для WebSocket toowork. Это требование не так, как протокол WebSocket требует hello первоначальное подтверждение установления связи toobe HTTP с протоколом обновления tooWebSocket как поле заголовка. Hello ниже приведен пример заголовка:

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

Другой причиной является то, что проверка работоспособности серверного шлюза приложений поддерживает только протоколы HTTP и HTTPS. Если hello внутренний сервер отвечает tooHTTP или зонды HTTPS, он берется из внутреннего пула.

## <a name="next-steps"></a>Дальнейшие действия

После изучения поддержка WebSocket, перейти слишком[создания шлюза приложения](application-gateway-create-gateway.md) tooget работы с WebSocket включены веб-приложения.

