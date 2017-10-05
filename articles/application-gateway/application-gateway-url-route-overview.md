---
title: "Общие сведения о маршрутизации содержимого на основе URL-адресов | Документация Майкрософт"
description: "Эта страница содержит общие сведения о маршрутизации содержимого шлюза приложений на основе URL-адресов, настройки UrlPathMap и правила PathBasedRouting."
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
ms.openlocfilehash: 75c3279d2d02cb3c6e949d191c88a1eb18b58a27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="5a15c-103">Общие сведения о маршрутизации на основе URL-путей</span><span class="sxs-lookup"><span data-stu-id="5a15c-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="5a15c-104">Маршрутизация на основе URL-путей позволяет направлять трафик в пулы тыловых серверов в зависимости от URL-путей поступающих запросов.</span><span class="sxs-lookup"><span data-stu-id="5a15c-104">URL Path Based Routing allows you to route traffic to back-end server pools based on URL Paths of the request.</span></span> 

<span data-ttu-id="5a15c-105">Один из сценариев — это маршрутизация запросов содержимого различных типов в различные пулы тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="5a15c-105">One of the scenarios is to route requests for different content types to different backend server pools.</span></span>

<span data-ttu-id="5a15c-106">В следующем примере шлюз приложений обслуживает трафик веб-сайта contoso.com с трех пулов тыловых серверов, например VideoServerPool, ImageServerPool и DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="5a15c-106">In the following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="5a15c-108">Запросы для http://contoso.com/video* направляются в VideoServerPool, а запросы для http://contoso.com/images* — в ImageServerPool.</span><span class="sxs-lookup"><span data-stu-id="5a15c-108">Requests for http://contoso.com/video* are routed to VideoServerPool, and http://contoso.com/images* are routed to ImageServerPool.</span></span> <span data-ttu-id="5a15c-109">Если ни один из шаблонов пути не подходит, выбирается пул DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="5a15c-109">DefaultServerPool is selected if none of the path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a15c-110">Правила обрабатываются в том порядке, в котором они указаны на портале.</span><span class="sxs-lookup"><span data-stu-id="5a15c-110">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="5a15c-111">Мы настоятельно рекомендуем в первую очередь настроить многосайтовые прослушиватели, чтобы настроить базовый прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="5a15c-111">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="5a15c-112">Это гарантирует, что трафик будет перенаправляться на правильный внутренний сервер.</span><span class="sxs-lookup"><span data-stu-id="5a15c-112">This ensures that traffic gets routed to the right back end.</span></span> <span data-ttu-id="5a15c-113">Если базовый прослушиватель стоит первым в списке и совпадает с входящим запросом, он будет обрабатываться прослушивателем.</span><span class="sxs-lookup"><span data-stu-id="5a15c-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="5a15c-114">Элемент конфигурации UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="5a15c-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="5a15c-115">Элемент urlPathMap используется для определения шаблонов пути при сопоставлении с пулом тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="5a15c-115">The urlPathMap element is used to specify Path patterns to back-end server pool mappings.</span></span> <span data-ttu-id="5a15c-116">Ниже приведен пример кода, который является фрагментом элемента urlPathMap из файла шаблона.</span><span class="sxs-lookup"><span data-stu-id="5a15c-116">The following code example is the snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="5a15c-117">Параметр PathPattern представляет список шаблонов пути для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="5a15c-117">PathPattern: This setting is a list of path patterns to match.</span></span> <span data-ttu-id="5a15c-118">Каждый шаблон должен начинаться с косой черты (/). Символ * может быть только в конце после косой черты.</span><span class="sxs-lookup"><span data-stu-id="5a15c-118">Each must start with / and the only place a "*" is allowed is at the end following a "/."</span></span> <span data-ttu-id="5a15c-119">Строка, передаваемая для сопоставления пути, не должна содержать никакого текста после первого символа ? или # — эти символы не допускаются.</span><span class="sxs-lookup"><span data-stu-id="5a15c-119">The string fed to the path matcher does not include any text after the first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="5a15c-120">Дополнительные сведения см. в статье [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) (Шаблон Resource Manager с использованием маршрутизации на основе URL-адресов).</span><span class="sxs-lookup"><span data-stu-id="5a15c-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="5a15c-121">Правило PathBasedRouting</span><span class="sxs-lookup"><span data-stu-id="5a15c-121">PathBasedRouting rule</span></span>

<span data-ttu-id="5a15c-122">Правило RequestRoutingRule типа PathBasedRouting используется для привязки прослушивателя к urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="5a15c-122">RequestRoutingRule of type PathBasedRouting is used to bind a listener to a urlPathMap.</span></span> <span data-ttu-id="5a15c-123">Все получаемые запросы для этого прослушивателя распределяются согласно политике, указанной в urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="5a15c-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="5a15c-124">Фрагмент правила PathBasedRouting:</span><span class="sxs-lookup"><span data-stu-id="5a15c-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5a15c-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a15c-125">Next steps</span></span>

<span data-ttu-id="5a15c-126">Ознакомившись с маршрутизацией на основе URL-адресов, создайте шлюз приложений с соответствующими правилами маршрутизации, как указано в статье о [создании шлюза приложений с помощью маршрутизации на основе URL-адресов](application-gateway-create-url-route-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="5a15c-126">After learning about URL-based content routing, go to [create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) to create an application gateway with URL routing rules.</span></span>
