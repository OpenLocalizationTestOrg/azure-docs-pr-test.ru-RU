---
title: "aaaHosting нескольких сайтов на использование шлюза приложений Azure | Документы Microsoft"
description: "Эта страница обзор поддержки нескольких сайтов шлюза приложения hello."
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
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="0bb7c-103">Размещение нескольких сайтов с помощью шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="0bb7c-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="0bb7c-104">Размещение нескольких сайтов позволяет tooconfigure более одного веб-приложения на hello одного экземпляра шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-104">Multiple site hosting enables you tooconfigure more than one web application on hello same application gateway instance.</span></span> <span data-ttu-id="0bb7c-105">Эта функция позволяет tooconfigure эффективнее топологию развертывания путем добавления шлюза приложений tooone too20 веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-105">This feature allows you tooconfigure a more efficient topology for your deployments by adding up too20 websites tooone application gateway.</span></span> <span data-ttu-id="0bb7c-106">Каждый сайт может направляться tooits владельцем внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-106">Each website can be directed tooits own backend pool.</span></span> <span data-ttu-id="0bb7c-107">В следующем примере hello шлюз приложений обслуживает трафик для contoso.com и fabrikam.com из двух серверных пулов, называется ContosoServerPool и FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-107">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="0bb7c-109">Правила обрабатываются в порядке hello, в котором они перечислены в портале hello.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-109">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="0bb7c-110">Это весьма рекомендуемые к использованию tooconfigure несколькими сайтами прослушивателей первый предыдущего tooconfiguring основные прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-110">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="0bb7c-111">Это позволит гарантировать завершение этого трафика получает перенаправленное toohello самому началу.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-111">This will ensure that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="0bb7c-112">Если базовый прослушиватель стоит первым в списке и совпадает с входящим запросом, он будет обрабатываться прослушивателем.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="0bb7c-113">Запросы для http://contoso.com перенаправленное tooContosoServerPool, и http://fabrikam.com это перенаправленное tooFabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-113">Requests for http://contoso.com are routed tooContosoServerPool, and http://fabrikam.com are routed tooFabrikamServerPool.</span></span>

<span data-ttu-id="0bb7c-114">Аналогичным образом две поддомены одного родительского домена может быть размещена на приветствия hello развертывания шлюза того же приложения.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-114">Similarly two subdomains of hello same parent domain can be hosted on hello same application gateway deployment.</span></span> <span data-ttu-id="0bb7c-115">К примерам использования поддоменов можно отнести http://blog.contoso.com и http://app.contoso.com, размещенные в одном развернутом шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="0bb7c-116">Заголовки узлов и указание имени сервера (SNI)</span><span class="sxs-lookup"><span data-stu-id="0bb7c-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="0bb7c-117">Существует три распространенных механизмов для включения нескольких узел размещения на hello же инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-117">There are three common mechanisms for enabling multiple site hosting on hello same infrastructure.</span></span>

1. <span data-ttu-id="0bb7c-118">Размещение нескольких веб-приложений с уникальным IP-адресом у каждого из них.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="0bb7c-119">Имя узла используйте, toohost несколько веб-приложений на hello же IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-119">Use host name toohost multiple web applications on hello same IP address.</span></span>
3. <span data-ttu-id="0bb7c-120">Использование разных портов toohost несколько веб-приложений на hello же IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-120">Use different ports toohost multiple web applications on hello same IP address.</span></span>

<span data-ttu-id="0bb7c-121">В настоящее время шлюз приложений получает один общедоступный IP-адрес, на котором он прослушивает трафик.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="0bb7c-122">Поэтому поддержка нескольких приложений, каждое из которых имеет собственный IP-адрес, сейчас не обеспечивается.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="0bb7c-123">Шлюз приложений поддерживает размещение нескольких приложений каждого прослушивание по различным портам, но этот сценарий требуют трафик tooaccept приложения hello нестандартные порты и часто не является требуемой конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require hello applications tooaccept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="0bb7c-124">Шлюз приложений использует протокол HTTP 1.1 toohost заголовки узлов более одного веб-сайта на hello же общедоступный IP-адрес и порт.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-124">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="0bb7c-125">Hello сайтов, размещенных на использование шлюза приложений также возможность поддержки разгрузки SSL с расширением TLS Указание имени сервера (SNI).</span><span class="sxs-lookup"><span data-stu-id="0bb7c-125">hello sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="0bb7c-126">Это означает, что этой hello клиента браузера и внутреннего веб-фермы должны поддерживать HTTP/1.1 и TLS модуля определению в RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-126">This scenario means that hello client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="0bb7c-127">Элемент конфигурации прослушивателя</span><span class="sxs-lookup"><span data-stu-id="0bb7c-127">Listener configuration element</span></span>

<span data-ttu-id="0bb7c-128">Существующие HTTPListener которой элемент конфигурации усиленной toosupport узла имя сервера имя указывает элементы и, используемой приложения шлюза tooroute трафика tooappropriate внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-128">Existing HTTPListener configuration element is enhanced toosupport host name and server name indication elements, which is used by application gateway tooroute traffic tooappropriate backend pool.</span></span> <span data-ttu-id="0bb7c-129">Hello следующий пример кода представляет фрагмент кода hello HTTP-прослушивателей элемента из файла шаблона.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-129">hello following code example is hello snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="0bb7c-130">Вы можете посетить [шаблона диспетчера ресурсов с помощью нескольких размещения сайта](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) для процесса tooend на основе шаблона развертывания.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end tooend template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="0bb7c-131">Правило маршрутизации</span><span class="sxs-lookup"><span data-stu-id="0bb7c-131">Routing rule</span></span>

<span data-ttu-id="0bb7c-132">Нет изменений в правила маршрутизации hello.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-132">There is no change required in hello routing rule.</span></span> <span data-ttu-id="0bb7c-133">Здравствуйте, правило маршрутизации «Basic» следует продолжить toobe выбран tootie hello подходящий сайт прослушивателя toohello соответствующего пула адресов серверной части.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-133">hello routing rule 'Basic' should continue toobe chosen tootie hello appropriate site listener toohello corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0bb7c-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0bb7c-134">Next steps</span></span>

<span data-ttu-id="0bb7c-135">После обучения о размещении нескольких сайта перейдите слишком[создания шлюза приложения с помощью нескольких размещения сайта](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate шлюза приложения с возможностью toosupport более одного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0bb7c-135">After learning about multiple site hosting, go too[create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate an application gateway with ability toosupport more than one web application.</span></span>

