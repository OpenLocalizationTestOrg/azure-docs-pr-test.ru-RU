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
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="85478-103">Общие сведения о поддержке WebSocket в шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="85478-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="85478-104">Шлюз приложений обеспечивает встроенную поддержку WebSocket независимо от размера.</span><span class="sxs-lookup"><span data-stu-id="85478-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="85478-105">Нет пользовательских параметр tooselectively enable или disable поддержка WebSocket.</span><span class="sxs-lookup"><span data-stu-id="85478-105">There is no user-configurable setting tooselectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="85478-106">Протокол WebSocket, стандартизированный в [RFC6455](https://tools.ietf.org/html/rfc6455), обеспечивает полнодуплексную связь между сервером и клиентом через длительное TCP-подключение.</span><span class="sxs-lookup"><span data-stu-id="85478-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="85478-107">Эта функция обеспечивает более интерактивного взаимодействия между hello веб-сервера и клиента hello, которое может быть двунаправленной без необходимости hello опроса, как требуется в реализации на основе HTTP.</span><span class="sxs-lookup"><span data-stu-id="85478-107">This feature allows for a more interactive communication between hello web server and hello client, which can be bidirectional without hello need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="85478-108">WebSocket имеет минимальные издержки в отличие от HTTP, и можно повторно использовать hello же TCP-подключение для нескольких запросов/ответов приведет к более эффективное использование ресурсов.</span><span class="sxs-lookup"><span data-stu-id="85478-108">WebSocket has low overhead unlike HTTP and can reuse hello same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="85478-109">Протоколы WebSocket спроектированный toowork превышают традиционных HTTP-порты 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="85478-109">WebSocket protocols are designed toowork over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="85478-110">Можно продолжить, используя стандартный прослушиватель HTTP на порт 80 или 443 tooreceive WebSocket трафика.</span><span class="sxs-lookup"><span data-stu-id="85478-110">You can continue using a standard HTTP listener on port 80 or 443 tooreceive WebSocket traffic.</span></span> <span data-ttu-id="85478-111">Трафик WebSocket —, направленной toohello WebSocket включается внутреннему серверу с помощью hello соответствующие внутреннего пула, как указано в правилах шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="85478-111">WebSocket traffic is then directed toohello WebSocket enabled backend server using hello appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="85478-112">Hello внутренний сервер должен отвечать зонды шлюза toohello приложения, которые описаны в hello [обзор проверки работоспособности](application-gateway-probe-overview.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="85478-112">hello backend server must respond toohello application gateway probes, which are described in hello [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="85478-113">Проверки работоспособности шлюза приложений выполняются только по протоколам HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="85478-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="85478-114">Каждого сервера базы данных, должен отвечать tooHTTP зонды для приложения tooroute WebSocket трафика toohello шлюза.</span><span class="sxs-lookup"><span data-stu-id="85478-114">Each backend server must respond tooHTTP probes for application gateway tooroute WebSocket traffic toohello server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="85478-115">Элемент конфигурации прослушивателя</span><span class="sxs-lookup"><span data-stu-id="85478-115">Listener configuration element</span></span>

<span data-ttu-id="85478-116">Существующего прослушивателя HTTP можно использовать toosupport трафика WebSocket.</span><span class="sxs-lookup"><span data-stu-id="85478-116">An existing HTTP listener can be used toosupport WebSocket traffic.</span></span> <span data-ttu-id="85478-117">Hello ниже приведен фрагмент HTTP-прослушивателей элемента из образец файла шаблона.</span><span class="sxs-lookup"><span data-stu-id="85478-117">hello following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="85478-118">Вам потребуется требуется прослушивателей HTTP и HTTPS, toosupport WebSocket и защита трафика WebSocket.</span><span class="sxs-lookup"><span data-stu-id="85478-118">You would need both HTTP and HTTPS listeners toosupport WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="85478-119">Аналогично можно использовать hello [портала](application-gateway-create-gateway-portal.md) или [PowerShell](application-gateway-create-gateway-arm.md) toocreate шлюза приложения с прослушивателями на порт 80 или 443 toosupport WebSocket трафик.</span><span class="sxs-lookup"><span data-stu-id="85478-119">Similarly you can use hello [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) toocreate an application gateway with listeners on port 80/443 toosupport WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="85478-120">BackendAddressPool, BackendHttpSetting и конфигурация правила маршрутизации</span><span class="sxs-lookup"><span data-stu-id="85478-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="85478-121">BackendAddressPool — используется toodefine внутренний пул с серверами WebSocket включены.</span><span class="sxs-lookup"><span data-stu-id="85478-121">A BackendAddressPool is used toodefine a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="85478-122">Hello backendHttpSetting определена внутренний порт 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="85478-122">hello backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="85478-123">свойства Hello сопоставление на основе файлов cookie и requestTimeouts не применимо tooWebSocket трафика.</span><span class="sxs-lookup"><span data-stu-id="85478-123">hello properties for cookie-based affinity and requestTimeouts are not relevant tooWebSocket traffic.</span></span> <span data-ttu-id="85478-124">Нет изменений в правила маршрутизации hello, «Basic» используется tootie hello соответствующего прослушивателя toohello соответствующий серверный пул адресов.</span><span class="sxs-lookup"><span data-stu-id="85478-124">There is no change required in hello routing rule, 'Basic' is used tootie hello appropriate listener toohello corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="85478-125">Сервер с поддержкой WebSocket</span><span class="sxs-lookup"><span data-stu-id="85478-125">WebSocket enabled backend</span></span>

<span data-ttu-id="85478-126">Серверной части должен иметь HTTP/HTTPS веб-сервер на hello настроен порт (обычно 80 или 443) для WebSocket toowork.</span><span class="sxs-lookup"><span data-stu-id="85478-126">Your backend must have a HTTP/HTTPS web server running on hello configured port (usually 80/443) for WebSocket toowork.</span></span> <span data-ttu-id="85478-127">Это требование не так, как протокол WebSocket требует hello первоначальное подтверждение установления связи toobe HTTP с протоколом обновления tooWebSocket как поле заголовка.</span><span class="sxs-lookup"><span data-stu-id="85478-127">This requirement is because WebSocket protocol requires hello initial handshake toobe HTTP with upgrade tooWebSocket protocol as a header field.</span></span> <span data-ttu-id="85478-128">Hello ниже приведен пример заголовка:</span><span class="sxs-lookup"><span data-stu-id="85478-128">hello following is an example of a header:</span></span>

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

<span data-ttu-id="85478-129">Другой причиной является то, что проверка работоспособности серверного шлюза приложений поддерживает только протоколы HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="85478-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="85478-130">Если hello внутренний сервер отвечает tooHTTP или зонды HTTPS, он берется из внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="85478-130">If hello backend server does not respond tooHTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85478-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="85478-131">Next steps</span></span>

<span data-ttu-id="85478-132">После изучения поддержка WebSocket, перейти слишком[создания шлюза приложения](application-gateway-create-gateway.md) tooget работы с WebSocket включены веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="85478-132">After learning about WebSocket support, go too[create an application gateway](application-gateway-create-gateway.md) tooget started with a WebSocket enabled web application.</span></span>

