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
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="c0101-103">Общие сведения о маршрутизации на основе URL-путей</span><span class="sxs-lookup"><span data-stu-id="c0101-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="c0101-104">URL-адрес на основе маршрутизации путей позволяет вам tooroute трафика tooback окончания пулов серверов на основании путей к URL-адрес запроса hello.</span><span class="sxs-lookup"><span data-stu-id="c0101-104">URL Path Based Routing allows you tooroute traffic tooback-end server pools based on URL Paths of hello request.</span></span> 

<span data-ttu-id="c0101-105">Одним из сценариев hello является tooroute запросов для различных типов содержимого toodifferent внутреннего сервера пулов.</span><span class="sxs-lookup"><span data-stu-id="c0101-105">One of hello scenarios is tooroute requests for different content types toodifferent backend server pools.</span></span>

<span data-ttu-id="c0101-106">В следующем примере hello, шлюз приложений обслуживающий трафик для contoso.com из трех серверных пулов например: VideoServerPool, ImageServerPool и DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="c0101-106">In hello following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="c0101-108">Запросы для http://contoso.com/video * перенаправленное tooVideoServerPool, и http://contoso.com/images * это перенаправленное tooImageServerPool.</span><span class="sxs-lookup"><span data-stu-id="c0101-108">Requests for http://contoso.com/video* are routed tooVideoServerPool, and http://contoso.com/images* are routed tooImageServerPool.</span></span> <span data-ttu-id="c0101-109">DefaultServerPool выбирается в том случае, если ни один из шаблонов путей hello соответствует.</span><span class="sxs-lookup"><span data-stu-id="c0101-109">DefaultServerPool is selected if none of hello path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0101-110">Правила обрабатываются в порядке hello, в котором они перечислены в портале hello.</span><span class="sxs-lookup"><span data-stu-id="c0101-110">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="c0101-111">Это весьма рекомендуемые к использованию tooconfigure несколькими сайтами прослушивателей первый предыдущего tooconfiguring основные прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="c0101-111">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="c0101-112">Это гарантирует завершение этого трафика получает перенаправленное toohello самому началу.</span><span class="sxs-lookup"><span data-stu-id="c0101-112">This ensures that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="c0101-113">Если базовый прослушиватель стоит первым в списке и совпадает с входящим запросом, он будет обрабатываться прослушивателем.</span><span class="sxs-lookup"><span data-stu-id="c0101-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="c0101-114">Элемент конфигурации UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="c0101-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="c0101-115">элемент urlPathMap Hello — сопоставления пула серверов используется toospecify путь шаблоны tooback-end.</span><span class="sxs-lookup"><span data-stu-id="c0101-115">hello urlPathMap element is used toospecify Path patterns tooback-end server pool mappings.</span></span> <span data-ttu-id="c0101-116">Hello следующий пример кода представляет фрагмент кода hello urlPathMap элемента из файла шаблона.</span><span class="sxs-lookup"><span data-stu-id="c0101-116">hello following code example is hello snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="c0101-117">PathPattern: Этот параметр является списком toomatch шаблонов пути.</span><span class="sxs-lookup"><span data-stu-id="c0101-117">PathPattern: This setting is a list of path patterns toomatch.</span></span> <span data-ttu-id="c0101-118">Каждый должно начинаться с / и hello единственное место «*» разрешается в hello окончания следовать «/».</span><span class="sxs-lookup"><span data-stu-id="c0101-118">Each must start with / and hello only place a "*" is allowed is at hello end following a "/."</span></span> <span data-ttu-id="c0101-119">Строка Hello переданы сопоставителе toohello путь не содержит текст после hello сначала? или # и эти символы не допускаются.</span><span class="sxs-lookup"><span data-stu-id="c0101-119">hello string fed toohello path matcher does not include any text after hello first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="c0101-120">Дополнительные сведения см. в статье [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) (Шаблон Resource Manager с использованием маршрутизации на основе URL-адресов).</span><span class="sxs-lookup"><span data-stu-id="c0101-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="c0101-121">Правило PathBasedRouting</span><span class="sxs-lookup"><span data-stu-id="c0101-121">PathBasedRouting rule</span></span>

<span data-ttu-id="c0101-122">RequestRoutingRule типа PathBasedRouting — используется toobind urlPathMap tooa прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="c0101-122">RequestRoutingRule of type PathBasedRouting is used toobind a listener tooa urlPathMap.</span></span> <span data-ttu-id="c0101-123">Все получаемые запросы для этого прослушивателя распределяются согласно политике, указанной в urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="c0101-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="c0101-124">Фрагмент правила PathBasedRouting:</span><span class="sxs-lookup"><span data-stu-id="c0101-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c0101-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0101-125">Next steps</span></span>

<span data-ttu-id="c0101-126">После изучения маршрутизации содержимого на основе URL-адрес, go слишком[создать с помощью маршрутизации на основе URL-адрес шлюза приложения](application-gateway-create-url-route-portal.md) toocreate шлюза с правилами маршрутизации URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="c0101-126">After learning about URL-based content routing, go too[create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) toocreate an application gateway with URL routing rules.</span></span>
