---
title: "aaaProtect веб-приложений с шлюз приложений Azure — PowerShell | Документы Microsoft"
description: "Это статье предоставлены рекомендации по tooconfigure веб-приложений, как назад конечного узлов шлюза существующего или нового приложения."
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
ms.date: 07/25/2017
ms.author: gwallace
ms.openlocfilehash: 2e5d3ba9acc2f60499e7102961e631ee3d44eede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-app-service-web-apps-with-application-gateway"></a><span data-ttu-id="0c38d-103">Настройка веб-приложений службы приложений с помощью шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="0c38d-103">Configure App Service Web Apps with Application Gateway</span></span> 

<span data-ttu-id="0c38d-104">Шлюз приложений позволяет toohave веб-приложение Azure или другой несколькими клиентами службы как член пула серверной части.</span><span class="sxs-lookup"><span data-stu-id="0c38d-104">Application gateway allows you toohave an Azure Web App or other multi-tenant service as a back-end pool member.</span></span> <span data-ttu-id="0c38d-105">В этой статье tooyou о tooconfigure веб-приложение Azure со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="0c38d-105">In this article, tooyou learn tooconfigure an Azure web app with Application Gateway.</span></span> <span data-ttu-id="0c38d-106">Hello в первом примере показано, как tooconfigure существующие toouse шлюза приложения как член пула серверной части веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0c38d-106">hello first example shows you how tooconfigure an existing application gateway toouse a web app as a back-end pool member.</span></span> <span data-ttu-id="0c38d-107">Hello во втором примере показано, как toocreate новый шлюз приложения с веб-приложения, как член пула серверной части.</span><span class="sxs-lookup"><span data-stu-id="0c38d-107">hello second example shows you how toocreate a new application gateway with a web app as a back-end pool member.</span></span>

## <a name="configure-a-web-app-behind-an-existing-application-gateway"></a><span data-ttu-id="0c38d-108">Настройка веб-приложения для имеющегося шлюза приложения</span><span class="sxs-lookup"><span data-stu-id="0c38d-108">Configure a web app behind an existing application gateway</span></span>

<span data-ttu-id="0c38d-109">Hello пример добавления веб-приложения как внутреннем пуле член tooan существующие приложения шлюз.</span><span class="sxs-lookup"><span data-stu-id="0c38d-109">hello following example adds a web app as a back-end pool member tooan existing application gateway.</span></span> <span data-ttu-id="0c38d-110">Оба hello коммутатора `-PickHostNamefromBackendHttpSettings`hello проверки конфигурации и `-PickHostNameFromBackendAddress` на серверной стороне http hello параметры должны задаваться в порядке для toowork приложения web.</span><span class="sxs-lookup"><span data-stu-id="0c38d-110">Both hello switch `-PickHostNamefromBackendHttpSettings`on hello Probe configuration and `-PickHostNameFromBackendAddress` on hello back-end http settings must be provided in order for web apps toowork.</span></span>

```powershell
# FQDN of hello web app
$webappFQDN = "<enter your webapp FQDN i.e mywebsite.azurewebsites.net>"

# Retrieve an existing application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName $rg.ResourceGroupName

# Define hello status codes toomatch for hello probe
$match=New-AzureRmApplicationGatewayProbeHealthResponseMatch -StatusCode 200-399

# Add a new probe toohello application gateway
Add-AzureRmApplicationGatewayProbeConfig -name webappprobe2 -ApplicationGateway $gw -Protocol Http -Path / -Interval 30 -Timeout 120 -UnhealthyThreshold 3 -PickHostNameFromBackendHttpSettings -Match $match

# Retrieve hello newly added probe
$probe = Get-AzureRmApplicationGatewayProbeConfig -name webappprobe2 -ApplicationGateway $gw

# Configure an existing backend http settings 
Set-AzureRmApplicationGatewayBackendHttpSettings -Name appGatewayBackendHttpSettings -ApplicationGateway $gw -PickHostNameFromBackendAddress -Port 80 -Protocol http -CookieBasedAffinity Disabled -RequestTimeout 30 -Probe $probe

# Add hello web app toohello backend pool
Set-AzureRmApplicationGatewayBackendAddressPool -Name appGatewayBackendPool -ApplicationGateway $gw -BackendIPAddresses $webappFQDN

# Update hello application gateway
Set-AzureRmApplicationGateway -ApplicationGateway $gw
```

## <a name="configure-a-web-application-behind-a-new-application-gateway"></a><span data-ttu-id="0c38d-111">Настройка веб-приложения для нового шлюза приложения</span><span class="sxs-lookup"><span data-stu-id="0c38d-111">Configure a web application behind a new application gateway</span></span>

<span data-ttu-id="0c38d-112">Этот сценарий выполняет развертывание веб-приложения с asp.net hello по началу работы веб-сайта и шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0c38d-112">This scenario deploys a web app with hello asp.net getting started website and an application gateway.</span></span>

```powershell
# Defines a variable for a dotnet get started web app repository location
$gitrepo="https://github.com/Azure-Samples/app-service-web-dotnet-get-started.git"

# Unique web app name
$webappname="mywebapp$(Get-Random)"

# Creates a resource group
$rg = New-AzureRmResourceGroup -Name ContosoRG -Location Eastus

# Create an App Service plan in Free tier.
New-AzureRmAppServicePlan -Name $webappname -Location EastUs -ResourceGroupName $rg.ResourceGroupName -Tier Free

# Creates a web app
$webapp = New-AzureRmWebApp -ResourceGroupName $rg.ResourceGroupName -Name $webappname -Location EastUs -AppServicePlan $webappname

# Configure GitHub deployment from your GitHub repo and deploy once tooweb app.
$PropertiesObject = @{
    repoUrl = "$gitrepo";
    branch = "master";
    isManualIntegration = "true";
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName $rg.ResourceGroupName -ResourceType Microsoft.Web/sites/sourcecontrols -ResourceName $webappname/web -ApiVersion 2015-08-01 -Force

# Creates a subnet for hello application gateway
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Creates a vnet for hello application gateway
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName $rg.ResourceGroupName -Location EastUs -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello subnet object for use later
$subnet=$vnet.Subnets[0]

# Create a public IP address
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName $rg.ResourceGroupName -name publicIP01 -location EastUs -AllocationMethod Dynamic

# Create a new IP configuration
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Create a backend pool with hello hostname of hello web app
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name appGatewayBackendPool -BackendIPAddresses $webapp.HostNames

# Define hello status codes toomatch for hello probe
$match = New-AzureRmApplicationGatewayProbeHealthResponseMatch -StatusCode 200-399

# Create a probe with hello PickHostNameFromBackendHttpSettings switch for web apps
$probeconfig = New-AzureRmApplicationGatewayProbeConfig -name webappprobe -Protocol Http -Path / -Interval 30 -Timeout 120 -UnhealthyThreshold 3 -PickHostNameFromBackendHttpSettings -Match $match

# Define hello backend http settings
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name appGatewayBackendHttpSettings -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120 -PickHostNameFromBackendAddress -Probe $probeconfig

# Create a new front-end port
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Create a new front end IP configuration
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Create a new listener using hello front-end ip configuration and port created earlier
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Create a new rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool 

# Define hello application gateway SKU toouse
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName $rg.ResourceGroupName -Location EastUs -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -Probes $probeconfig -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="0c38d-113">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="0c38d-113">Get application gateway DNS name</span></span>

<span data-ttu-id="0c38d-114">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="0c38d-114">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="0c38d-115">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="0c38d-115">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="0c38d-116">tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0c38d-116">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="0c38d-117">toocreate hello псевдоним, получить сведения о hello шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений.</span><span class="sxs-lookup"><span data-stu-id="0c38d-117">toocreate hello alias, retrieve hello details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="0c38d-118">Это можно сделать с помощью Azure DNS или других поставщиков DNS, при создании записи CNAME, точек toohello [общедоступный IP-адрес](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="0c38d-118">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points toohello [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="0c38d-119">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0c38d-119">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : eastus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="0c38d-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0c38d-120">Next steps</span></span>

<span data-ttu-id="0c38d-121">Узнайте, как tooconfigure перенаправление по следующему адресу: [Настройка перенаправления на использование шлюза приложений с помощью PowerShell](application-gateway-configure-redirect-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0c38d-121">Learn how tooconfigure redirection by visiting: [Configure redirection on Application Gateway with PowerShell](application-gateway-configure-redirect-powershell.md).</span></span>
