---
title: "Поддержка WebSocket в шлюзе приложений Azure| Документация Майкрософт"
description: "Здесь представлен обзор поддержки WebSocket в шлюзе приложений."
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
ms.openlocfilehash: 75b06ddd02da231b7813c609c848c75e42116da5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="db32f-103">Общие сведения о поддержке WebSocket в шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="db32f-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="db32f-104">Шлюз приложений обеспечивает встроенную поддержку WebSocket независимо от размера.</span><span class="sxs-lookup"><span data-stu-id="db32f-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="db32f-105">Настраиваемый пользователем параметр для выборочного включения или отключения поддержки WebSocket отсутствует.</span><span class="sxs-lookup"><span data-stu-id="db32f-105">There is no user-configurable setting to selectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="db32f-106">Протокол WebSocket, стандартизированный в [RFC6455](https://tools.ietf.org/html/rfc6455), обеспечивает полнодуплексную связь между сервером и клиентом через длительное TCP-подключение.</span><span class="sxs-lookup"><span data-stu-id="db32f-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="db32f-107">Эта функция обеспечивает лучшее интерактивное взаимодействие между веб-сервером и клиентом, которое может быть двунаправленным, без необходимости выполнять опрос, как в реализациях на основе HTTP.</span><span class="sxs-lookup"><span data-stu-id="db32f-107">This feature allows for a more interactive communication between the web server and the client, which can be bidirectional without the need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="db32f-108">В отличие от HTTP протокол WebSocket обеспечивает низкие издержки и может повторно использовать одно и то же TCP-подключение для нескольких запросов и ответов, благодаря чему ресурсы используются более эффективно.</span><span class="sxs-lookup"><span data-stu-id="db32f-108">WebSocket has low overhead unlike HTTP and can reuse the same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="db32f-109">Протоколы WebSocket работают через традиционные HTTP-порты 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="db32f-109">WebSocket protocols are designed to work over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="db32f-110">Вы можете продолжать использовать стандартный прослушиватель HTTPListener на порте 80 или 443 для получения трафика WebSocket.</span><span class="sxs-lookup"><span data-stu-id="db32f-110">You can continue using a standard HTTP listener on port 80 or 443 to receive WebSocket traffic.</span></span> <span data-ttu-id="db32f-111">Затем этот трафик направляется на внутренний сервер с поддержкой WebSocket с использованием соответствующего серверного пула, как определено в правилах шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="db32f-111">WebSocket traffic is then directed to the WebSocket enabled backend server using the appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="db32f-112">Внутренний сервер должен отвечать на проверки работоспособности шлюза приложений. Описание проверок см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db32f-112">The backend server must respond to the application gateway probes, which are described in the [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="db32f-113">Проверки работоспособности шлюза приложений выполняются только по протоколам HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="db32f-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="db32f-114">Каждый внутренний сервер должен отвечать на проверки HTTP шлюза приложений для маршрутизации трафика WebSocket на сервер.</span><span class="sxs-lookup"><span data-stu-id="db32f-114">Each backend server must respond to HTTP probes for application gateway to route WebSocket traffic to the server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="db32f-115">Элемент конфигурации прослушивателя</span><span class="sxs-lookup"><span data-stu-id="db32f-115">Listener configuration element</span></span>

<span data-ttu-id="db32f-116">Для поддержки трафика WebSocket можно использовать имеющийся прослушиватель HTTPListener.</span><span class="sxs-lookup"><span data-stu-id="db32f-116">An existing HTTP listener can be used to support WebSocket traffic.</span></span> <span data-ttu-id="db32f-117">Ниже приведен фрагмент кода с элементом httpListeners из примера файла шаблона.</span><span class="sxs-lookup"><span data-stu-id="db32f-117">The following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="db32f-118">Для поддержки и защиты трафика WebSocket необходимы прослушиватели HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="db32f-118">You would need both HTTP and HTTPS listeners to support WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="db32f-119">Чтобы создать шлюз приложений с прослушивателями на порте 80 или 443 для поддержки трафика WebSocket, можно использовать [портал](application-gateway-create-gateway-portal.md) или [PowerShell](application-gateway-create-gateway-arm.md)</span><span class="sxs-lookup"><span data-stu-id="db32f-119">Similarly you can use the [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) to create an application gateway with listeners on port 80/443 to support WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="db32f-120">BackendAddressPool, BackendHttpSetting и конфигурация правила маршрутизации</span><span class="sxs-lookup"><span data-stu-id="db32f-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="db32f-121">Для определения серверного пула с серверами с поддержкой WebSocket используется параметр BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="db32f-121">A BackendAddressPool is used to define a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="db32f-122">Параметр backendHttpSetting определяется с внутренним портом 80 или 443.</span><span class="sxs-lookup"><span data-stu-id="db32f-122">The backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="db32f-123">Свойства для сходства на основе файлов cookie и requestTimeouts не связаны с трафиком WebSocket.</span><span class="sxs-lookup"><span data-stu-id="db32f-123">The properties for cookie-based affinity and requestTimeouts are not relevant to WebSocket traffic.</span></span> <span data-ttu-id="db32f-124">Чтобы привязать соответствующий прослушиватель к нужному серверному пулу адресов, в базовое правило маршрутизации не нужно вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="db32f-124">There is no change required in the routing rule, 'Basic' is used to tie the appropriate listener to the corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="db32f-125">Сервер с поддержкой WebSocket</span><span class="sxs-lookup"><span data-stu-id="db32f-125">WebSocket enabled backend</span></span>

<span data-ttu-id="db32f-126">Для работы сервера с поддержкой WebSocket необходимо, чтобы веб-сервер HTTP или HTTPS работал на настроенном порте (обычно 80 или 443).</span><span class="sxs-lookup"><span data-stu-id="db32f-126">Your backend must have a HTTP/HTTPS web server running on the configured port (usually 80/443) for WebSocket to work.</span></span> <span data-ttu-id="db32f-127">Это требование связано с тем, что протокол WebSocket требует первоначального подтверждения в виде обновления протокола HTTP до WebSocket. При этом последний должен быть указан как поле заголовка.</span><span class="sxs-lookup"><span data-stu-id="db32f-127">This requirement is because WebSocket protocol requires the initial handshake to be HTTP with upgrade to WebSocket protocol as a header field.</span></span> <span data-ttu-id="db32f-128">Ниже приведен пример заголовка:</span><span class="sxs-lookup"><span data-stu-id="db32f-128">The following is an example of a header:</span></span>

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

<span data-ttu-id="db32f-129">Другой причиной является то, что проверка работоспособности серверного шлюза приложений поддерживает только протоколы HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="db32f-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="db32f-130">Если внутренний сервер не отвечает на проверки по протоколу HTTP или HTTPS, он удаляется из внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="db32f-130">If the backend server does not respond to HTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db32f-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="db32f-131">Next steps</span></span>

<span data-ttu-id="db32f-132">Ознакомившись с поддержкой протокола WebSocket, приступите к [созданию шлюза приложений](application-gateway-create-gateway.md) , чтобы начать работу с веб-приложением с поддержкой WebSocket.</span><span class="sxs-lookup"><span data-stu-id="db32f-132">After learning about WebSocket support, go to [create an application gateway](application-gateway-create-gateway.md) to get started with a WebSocket enabled web application.</span></span>

