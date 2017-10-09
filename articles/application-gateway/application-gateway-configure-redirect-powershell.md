---
title: "перенаправление aaaConfigure для шлюза приложения Azure — PowerShell | Документы Microsoft"
description: "На этой странице представлены сценарии tooconfigure перенаправления для шлюза приложения, использование PowerShell"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: gwallace
ms.openlocfilehash: 1abe095287b001e501465ced05e171326bb29b5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-redirection-on-application-gateway-with-powershell"></a><span data-ttu-id="3b723-103">Настройка перенаправления в шлюзе приложений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b723-103">Configure redirection on Application Gateway with PowerShell</span></span>

<span data-ttu-id="3b723-104">Шлюз приложений поддерживает hello возможность tooredirect трафика в зависимости от определенной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3b723-104">Application gateway supports hello ability tooredirect traffic based on a defined configuration.</span></span> <span data-ttu-id="3b723-105">Дополнительные о перенаправлении в общие посещение toolearn [Обзор перенаправления шлюза приложения](application-gateway-redirect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b723-105">toolearn more about redirection in general visit, [Application Gateway redirect overview](application-gateway-redirect-overview.md).</span></span> <span data-ttu-id="3b723-106">В этой статье приведены примеры tooHTTPS перенаправление HTTP, путь к основе перенаправляет перенаправление нескольких сайтов и перенаправляет tooexternal сайтов.</span><span class="sxs-lookup"><span data-stu-id="3b723-106">This article provides examples of HTTP tooHTTPS redirection, path based redirects, multi-site redirects, and redirects tooexternal sites.</span></span>

## <a name="http-toohttps-redirect-on-an-existing-application-gateway"></a><span data-ttu-id="3b723-107">Перенаправления HTTP tooHTTPS в существующего шлюза приложения</span><span class="sxs-lookup"><span data-stu-id="3b723-107">HTTP tooHTTPS redirect on an existing application gateway</span></span>

<span data-ttu-id="3b723-108">Hello следующий пример создает новый прослушиватель HTTP на порт 80 tooredirect запросов toohello существующего прослушивателя на порте 443.</span><span class="sxs-lookup"><span data-stu-id="3b723-108">hello following example creates a new HTTP listener on port 80 tooredirect requests toohello existing listener on port 443.</span></span>

```powershell
# Get hello application gateway
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG

# Get hello existing HTTPS listener
$httpslistener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener -ApplicationGateway $gw

# Get hello existing front end IP configuration
$fipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig -Name appgatewayfrontendip -ApplicationGateway $gw

# Add a new front end port toosupport HTTP traffic
Add-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2  -Port 80 -ApplicationGateway $gw

# Get hello recently created port
$fp = Get-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2 -ApplicationGateway $gw

# Create a new HTTP listener using hello port created earlier
Add-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2  -Protocol Http -FrontendPort $fp -FrontendIPConfiguration $fipconfig -ApplicationGateway $gw 

# Get hello new listener
$listener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2 -ApplicationGateway $gw

# Add a redirection configuration using a permanent redirect and targeting hello existing listener
Add-AzureRmApplicationGatewayRedirectConfiguration -Name redirectHttptoHttps -RedirectType Permanent -TargetListener $httpslistener -IncludePath $true -IncludeQueryString $true -ApplicationGateway $gw

# Get hello redirect configuration
$redirectconfig = Get-AzureRmApplicationGatewayRedirectConfiguration -Name redirectHttptoHttps -ApplicationGateway $gw


# Add a new rule toohandle hello redirect and use hello new listener
Add-AzureRmApplicationGatewayRequestRoutingRule -Name rule02 -RuleType Basic -HttpListener $listener -RedirectConfiguration $redirectconfig -ApplicationGateway $gw

# Update hello application gateway
Set-AzureRmApplicationGateway -ApplicationGateway $gw 
```

<span data-ttu-id="3b723-109">После обновления шлюза приложения hello, тестирование нового прослушивателя hello через порт 80.</span><span class="sxs-lookup"><span data-stu-id="3b723-109">Once hello application gateway is updated, test hello new listener on port 80.</span></span>  <span data-ttu-id="3b723-110">Hello следующий пример демонстрирует использование `curl` тестирования hello перенаправления.</span><span class="sxs-lookup"><span data-stu-id="3b723-110">hello following example shows using `curl` test hello redirection.</span></span>

```
curl http://40.69.161.221 -i
HTTP/1.1 301 Moved Permanently
Content-Type: text/html; charset=UTF-8
Location: https://40.69.161.221/
Server: Microsoft-IIS/10.0
Date: Tue, 11 Jul 2017 20:54:00 GMT
Content-Length: 145

<head><title>Document Moved</title></head>
<body><h1>Object Moved</h1>This document may be found <a HREF="https://40.69.161.221/">here</a></body>
```

## <a name="path-based-redirect"></a><span data-ttu-id="3b723-111">Перенаправление на основе путей</span><span class="sxs-lookup"><span data-stu-id="3b723-111">Path based redirect</span></span>

<span data-ttu-id="3b723-112">Следующий пример Hello создает на основе существующего шлюза приложения, который перенаправляет только трафик, соответствующие hello определенный путь URL-адрес нового прослушивателя и правила на основе пути.</span><span class="sxs-lookup"><span data-stu-id="3b723-112">hello following example creates a new listener and a path based rule on an existing application gateway that redirects only traffic meeting hello specific url path.</span></span>

```powershell
# Get hello application gateway
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG

# Get hello existing HTTPS listener
$httpslistener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener -ApplicationGateway $gw

# Get hello existing front end IP configuration
$fipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig -Name appgatewayfrontendip -ApplicationGateway $gw

# Add a new front end port toosupport HTTP traffic
Add-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2  -Port 80 -ApplicationGateway $gw

# Get hello recently created port
$fp = Get-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2 -ApplicationGateway $gw

# Create a new HTTP listener using hello port created earlier
Add-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2  -Protocol Http -FrontendPort $fp -FrontendIPConfiguration $fipconfig -ApplicationGateway $gw 

# Get hello new listener
$listener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2 -ApplicationGateway $gw

# Add a redirection configuration using a permanent redirect and targeting hello existing listener
$redirectconfig = Get-AzureRmApplicationGatewayRedirectConfiguration -Name redirectpath6 -ApplicationGateway $gw

# Retrieve hello existing backend http settings toobe used
$poolSetting = Get-AzureRmApplicationGatewayBackendHttpSettings -Name "appGatewayBackendHttpSettings" -ApplicationGateway $gw

# Retrieve an existing backend pool
$pool = Get-AzureRmApplicationGatewayBackendAddressPool -Name appGatewayBackendPool -ApplicationGateway $gw

# Create a new path based rule
$pathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule6" -Paths "/image/*" -BackendAddressPool $pool -BackendHttpSettings $poolSetting

# Create a path map tooadd toohello rule
Add-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $pathRule -DefaultBackendAddressPool $pool -DefaultBackendHttpSettings $poolSetting -ApplicationGateway $gw

# Retrieve hello url path map created
$urlPathMap = Get-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -ApplicationGateway $gw

# Add a new rule toohandle hello redirect and use hello new listener
Add-AzureRmApplicationGatewayRequestRoutingRule -Name "rule6" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap -RedirectConfiguration $redirectconfig -ApplicationGateway $gw

# Update hello application gateway
Set-AzureRmApplicationGateway -ApplicationGateway $gw 
```

## <a name="multi-site-redirect"></a><span data-ttu-id="3b723-113">Перенаправление на несколько сайтов</span><span class="sxs-lookup"><span data-stu-id="3b723-113">Multi-site redirect</span></span>

<span data-ttu-id="3b723-114">Hello следующий пример создает новый шлюз приложения с 2 прослушиватели несколькими сайтами через порт 80.</span><span class="sxs-lookup"><span data-stu-id="3b723-114">hello following example creates a new application gateway with 2 multi-site listeners on port 80.</span></span> <span data-ttu-id="3b723-115">прослушиватели Hello предназначены для adatum.com и adatum.org. Правило перенаправления трафика tooredirect создаются из adatum.org tooadatum.com. Дополнительная настройка не требуется Настройка CNAME псевдонимы toohello приложения открытый IP-адрес шлюза, Дополнительные сведения о делегировании tooAzure вашего домена DNS, а также создание CNAME записями для вашего домена, [делегировать домена tooAzure DNS](../dns/dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="3b723-115">hello listeners are for adatum.com and adatum.org. A redirect rule is created tooredirect traffic from adatum.org tooadatum.com. Additional configuration is required for configuring CNAME aliases toohello application gateway public IP address, for more information on delegating your domain tooAzure DNS and creating CNAME records for your domain visit, [Delegate a domain tooAzure DNS](../dns/dns-delegate-domain-azure-dns.md).</span></span>

```powershell
# Create a new resource group for hello application gateway
New-AzureRmResourceGroup -Name appgw-rg -Location "East US"

# Create a subnet configuration object for hello application gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your application gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet

# Create a public IP address for use with hello application gateway. Defining hello domainnamelabel during creation is not supported for use with application gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "East US" -AllocationMethod Dynamic

# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $vnet.Subnets[0]

# Create a backend pool toohold hello addresses or NICs for hello application that application gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 80

# Create a frontend IP configuration tooassociate hello public IP address with hello application gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Create hello HTTP listener for hello application gateway for adatum.com. Assign hello front-end ip configuration, and port.
$listener1 = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp -HostName adatum.com

# Create hello HTTP listener for hello application gateway for adatum.org this listener will redirect toohello abc.com listener. Assign hello front-end ip configuration, and port.
$listener2 = New-AzureRmApplicationGatewayHttpListener -Name listener02 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp -HostName adatum.org

# Create hello redirect configuration that will point traffic toohello 
$redirectconfig = New-AzureRmApplicationGatewayRedirectConfiguration -Name redirectOrgtoCom -RedirectType Found -TargetListener $listener1 -IncludePath $true -IncludeQueryString $true

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule1 = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -HttpListener $listener1 -BackendHttpSettings $poolSetting -BackendAddressPool $pool

#Create a load balancer routing rule that redirects traffic toohello adatum.com listener
$rule2 = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule02 -RuleType Basic -HttpListener $listener2 -RedirectConfiguration $redirectconfig

# Configure hello SKU of hello application gateway
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Medium -Tier Standard -Capacity 2

# Create hello application gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener,$listener2 -RequestRoutingRules $rule1,$rule2 -RedirectConfigurations $redirectconfig -Sku $sku
```

## <a name="redirect-tooan-external-site"></a><span data-ttu-id="3b723-116">Внешний узел tooan перенаправления</span><span class="sxs-lookup"><span data-stu-id="3b723-116">Redirect tooan external site</span></span>

<span data-ttu-id="3b723-117">Hello примере перенаправляет трафик, поступающий на hello приложения tooan внешнего веб-сайта шлюза (bing.com).</span><span class="sxs-lookup"><span data-stu-id="3b723-117">hello following example redirects traffic coming into hello application gateway tooan external website (bing.com).</span></span> <span data-ttu-id="3b723-118">При использовании hello `TargetUrl` hello коммутатора `IncludePath` и `IncludeQuery` ключи не допускаются.</span><span class="sxs-lookup"><span data-stu-id="3b723-118">When using hello `TargetUrl` switch hello `IncludePath` and `IncludeQuery` switches are not allowed.</span></span>

```powershell
# Create a new resource group for hello application gateway
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"

# Create a subnet configuration object for hello application gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your application gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet

# Create a public IP address for use with hello application gateway. Defining hello domainnamelabel during creation is not supported for use with application gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic

# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $vnet.Subnets[0]

# Create a backend pool toohold hello addresses or NICs for hello application that application gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 80

# Create a frontend IP configuration tooassociate hello public IP address with hello application gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Create hello HTTP listener for hello application gateway. Assign hello front-end ip configuration, and port.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp 

# Create hello redirect configuration that will point traffic toohello 
$redirectconfig = New-AzureRmApplicationGatewayRedirectConfiguration -Name myredirect -RedirectType Temporary -TargetUrl "http://bing.com" -IncludePath $true -IncludeQueryString $true

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -HttpListener $listener -RedirectConfiguration $redirectconfig 

# Configure hello SKU of hello application gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Create hello application gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -RedirectConfigurations $redirectconfig -Sku $sku
```

## <a name="next-steps"></a><span data-ttu-id="3b723-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b723-119">Next steps</span></span>

<span data-ttu-id="3b723-120">Посетите [Настройка tooend окончания SSL с помощью шлюза приложения с помощью PowerShell](application-gateway-end-to-end-ssl-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="3b723-120">Visit [configure end tooend SSL with application gateway using PowerShell](application-gateway-end-to-end-ssl-powershell.md)</span></span>
