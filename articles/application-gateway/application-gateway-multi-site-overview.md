---
title: "Размещение нескольких сайтов в шлюзе приложений Azure | Документация Майкрософт"
description: "На этой странице предоставлен обзор поддержки нескольких сайтов в шлюзе приложений."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 645f68d836babf11f32fc391e6dacc9430f0070c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="69772-103">Размещение нескольких сайтов с помощью шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="69772-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="69772-104">Размещение нескольких сайтов позволяет настроить в одном экземпляре шлюза приложений не одно, а несколько веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="69772-104">Multiple site hosting enables you to configure more than one web application on the same application gateway instance.</span></span> <span data-ttu-id="69772-105">Эта функция позволяет настроить более эффективную топологию развернутых служб, добавляя до 20 веб-сайтов в один шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="69772-105">This feature allows you to configure a more efficient topology for your deployments by adding up to 20 websites to one application gateway.</span></span> <span data-ttu-id="69772-106">Каждый веб-сайт может быть направлен в свой собственный внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="69772-106">Each website can be directed to its own backend pool.</span></span> <span data-ttu-id="69772-107">В следующем примере шлюз приложений обслуживает трафик сайтов contoso.com и fabrikam.com с помощью двух внутренних пулов серверов: ContosoServerPool и FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="69772-107">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="69772-109">Правила обрабатываются в том порядке, в котором они указаны на портале.</span><span class="sxs-lookup"><span data-stu-id="69772-109">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="69772-110">Мы настоятельно рекомендуем в первую очередь настроить многосайтовые прослушиватели, чтобы настроить базовый прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="69772-110">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="69772-111">Это позволит гарантировать, что трафик будет перенаправлен на правильный внутренний сервер.</span><span class="sxs-lookup"><span data-stu-id="69772-111">This will ensure that traffic gets routed to the right back end.</span></span> <span data-ttu-id="69772-112">Если базовый прослушиватель стоит первым в списке и совпадает с входящим запросом, он будет обрабатываться прослушивателем.</span><span class="sxs-lookup"><span data-stu-id="69772-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="69772-113">Запросы к http://contoso.com будут направляться в пул ContosoServerPool, а запросы к http://fabrikam.com — в пул FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="69772-113">Requests for http://contoso.com are routed to ContosoServerPool, and http://fabrikam.com are routed to FabrikamServerPool.</span></span>

<span data-ttu-id="69772-114">Точно так же в одном развернутом шлюзе приложений можно разместить два поддомена одного родительского домена.</span><span class="sxs-lookup"><span data-stu-id="69772-114">Similarly two subdomains of the same parent domain can be hosted on the same application gateway deployment.</span></span> <span data-ttu-id="69772-115">К примерам использования поддоменов можно отнести http://blog.contoso.com и http://app.contoso.com, размещенные в одном развернутом шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="69772-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="69772-116">Заголовки узлов и указание имени сервера (SNI)</span><span class="sxs-lookup"><span data-stu-id="69772-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="69772-117">Существует три распространенных механизма, обеспечивающих размещение нескольких сайтов в одной инфраструктуре:</span><span class="sxs-lookup"><span data-stu-id="69772-117">There are three common mechanisms for enabling multiple site hosting on the same infrastructure.</span></span>

1. <span data-ttu-id="69772-118">Размещение нескольких веб-приложений с уникальным IP-адресом у каждого из них.</span><span class="sxs-lookup"><span data-stu-id="69772-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="69772-119">Использование имени узла для размещения нескольких веб-приложений на одном IP-адресе.</span><span class="sxs-lookup"><span data-stu-id="69772-119">Use host name to host multiple web applications on the same IP address.</span></span>
3. <span data-ttu-id="69772-120">Использование разных портов для размещения нескольких веб-приложений на одном IP-адресе.</span><span class="sxs-lookup"><span data-stu-id="69772-120">Use different ports to host multiple web applications on the same IP address.</span></span>

<span data-ttu-id="69772-121">В настоящее время шлюз приложений получает один общедоступный IP-адрес, на котором он прослушивает трафик.</span><span class="sxs-lookup"><span data-stu-id="69772-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="69772-122">Поэтому поддержка нескольких приложений, каждое из которых имеет собственный IP-адрес, сейчас не обеспечивается.</span><span class="sxs-lookup"><span data-stu-id="69772-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="69772-123">Шлюз приложений поддерживает размещение нескольких приложений, которые прослушивают разные порты. В рамках этого сценария приложениям нужно принимать трафик через нестандартные порты, что часто является нежелательным для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="69772-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require the applications to accept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="69772-124">Шлюз приложений использует заголовки узлов HTTP 1.1 для размещения нескольких веб-сайтов на одном общедоступном IP-адресе и порте.</span><span class="sxs-lookup"><span data-stu-id="69772-124">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="69772-125">Сайты, размещенные в шлюзе приложений, могут также поддерживать разгрузку SSL с использованием расширения TLS для указания имени сервера (SNI).</span><span class="sxs-lookup"><span data-stu-id="69772-125">The sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="69772-126">В рамках этого сценария это значит, что браузер клиента и внутренняя веб-ферма должны поддерживать HTTP/1.1 и расширение TLS, как определено в стандарте RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="69772-126">This scenario means that the client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="69772-127">Элемент конфигурации прослушивателя</span><span class="sxs-lookup"><span data-stu-id="69772-127">Listener configuration element</span></span>

<span data-ttu-id="69772-128">Существующий элемент конфигурации HTTPListener усовершенствован для поддержки элементов имени узла и указания имени сервера, используемых шлюзом приложений для маршрутизации трафика в соответствующий внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="69772-128">Existing HTTPListener configuration element is enhanced to support host name and server name indication elements, which is used by application gateway to route traffic to appropriate backend pool.</span></span> <span data-ttu-id="69772-129">Ниже приведен пример кода, который является фрагментом элемента HttpListeners из файла шаблона.</span><span class="sxs-lookup"><span data-stu-id="69772-129">The following code example is the snippet of HttpListeners element from template file.</span></span>

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

<span data-ttu-id="69772-130">Комплексное развертывание с помощью шаблона можно изучить на примере [шаблона Resource Manager, использующего размещение нескольких сайтов](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting).</span><span class="sxs-lookup"><span data-stu-id="69772-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end to end template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="69772-131">Правило маршрутизации</span><span class="sxs-lookup"><span data-stu-id="69772-131">Routing rule</span></span>

<span data-ttu-id="69772-132">Правило маршрутизации изменять не нужно.</span><span class="sxs-lookup"><span data-stu-id="69772-132">There is no change required in the routing rule.</span></span> <span data-ttu-id="69772-133">Следует все так же выбрать базовое правило маршрутизации, чтобы привязать соответствующий сайт прослушивателя к нужному внутреннему пулу адресов.</span><span class="sxs-lookup"><span data-stu-id="69772-133">The routing rule 'Basic' should continue to be chosen to tie the appropriate site listener to the corresponding backend address pool.</span></span>

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a><span data-ttu-id="69772-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69772-134">Next steps</span></span>

<span data-ttu-id="69772-135">Изучив размещение нескольких сайтов, перейдите к [созданию шлюза приложений с использованием размещения нескольких сайтов](application-gateway-create-multisite-azureresourcemanager-powershell.md) , чтобы создать шлюз приложений с возможностью поддержки нескольких веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="69772-135">After learning about multiple site hosting, go to [create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) to create an application gateway with ability to support more than one web application.</span></span>

