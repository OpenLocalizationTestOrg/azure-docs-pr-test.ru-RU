---
title: "Настройка политики SSL на шлюзе приложений Azure с помощью PowerShell | Документация Майкрософт"
description: "На этой странице представлены инструкции по настройке политики SSL на шлюзе приложений Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: ece2549a607ffa06602c26cf77db93f67112d029
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="configure-ssl-policy-versions-and-cipher-suites-on-application-gateway"></a><span data-ttu-id="61328-103">Настройка версий политики SSL и комплектов шифров на шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="61328-103">Configure SSL policy versions and cipher suites on Application Gateway</span></span>

<span data-ttu-id="61328-104">Узнайте, как настроить версии политики SSL и комплекты шифров на шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="61328-104">Learn how to configure SSL policy versions and cipher suites on Application Gateway.</span></span> <span data-ttu-id="61328-105">Можно воспользоваться [списком стандартных политик](#predefined-ssl-policies), в котором содержатся различные конфигурации версий политики SSL и разрешенные комплекты шифров.</span><span class="sxs-lookup"><span data-stu-id="61328-105">You can select from a [list of predefined policies](#predefined-ssl-policies) that contain different configurations of SSL policy versions and enabled cipher suites.</span></span> <span data-ttu-id="61328-106">Также можно определить [пользовательскую политику SSL](#configure-a-custom-ssl-policy) в соответствии с требованиями.</span><span class="sxs-lookup"><span data-stu-id="61328-106">You also have the ability to define a [custom SSL policy](#configure-a-custom-ssl-policy) based on your requirements.</span></span>

## <a name="get-available-ssl-options"></a><span data-ttu-id="61328-107">Получение доступных параметров SSL</span><span class="sxs-lookup"><span data-stu-id="61328-107">Get available SSL options</span></span>

<span data-ttu-id="61328-108">Командлет `Get-AzureRMApplicationGatewayAvailableSslOptions` позволяет получить список доступных стандартных политик, доступных комплектов шифров и версий протокола, которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="61328-108">The `Get-AzureRMApplicationGatewayAvailableSslOptions` cmdlet provides a listing of available pre-defined policies, available cipher suites, and protocol versions that can be configured.</span></span> <span data-ttu-id="61328-109">Ниже приведен пример результата выполнения командлета.</span><span class="sxs-lookup"><span data-stu-id="61328-109">The following example shows an example output from running the cmdlet.</span></span>

```
DefaultPolicy: AppGwSslPolicy20150501
PredefinedPolicies:
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20150501
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401S

AvailableCipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
    TLS_RSA_WITH_AES_128_GCM_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA256
    TLS_RSA_WITH_AES_128_CBC_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA
    TLS_RSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_3DES_EDE_CBC_SHA
    TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

AvailableProtocols:
    TLSv1_0
    TLSv1_1
    TLSv1_2
```

## <a name="list-pre-defined-ssl-policies"></a><span data-ttu-id="61328-110">Список стандартных политик SSL</span><span class="sxs-lookup"><span data-stu-id="61328-110">List pre-defined SSL Policies</span></span>

<span data-ttu-id="61328-111">В составе шлюза приложений имеется 3 стандартные политики, которыми можно воспользоваться.</span><span class="sxs-lookup"><span data-stu-id="61328-111">Application gateway comes with 3 pre-defined policies that can be used.</span></span> <span data-ttu-id="61328-112">Командлет `Get-AzureRmApplicationGatewaySslPredefinedPolicy` извлекает эти политики.</span><span class="sxs-lookup"><span data-stu-id="61328-112">The `Get-AzureRmApplicationGatewaySslPredefinedPolicy` cmdlet retrieves these policies.</span></span> <span data-ttu-id="61328-113">В каждой политике включены разные версии протокола SSL и комплекты шифров.</span><span class="sxs-lookup"><span data-stu-id="61328-113">Each policy has different protocol versions and cipher suites enabled.</span></span> <span data-ttu-id="61328-114">Эти стандартные политики можно использовать для быстрой настройки политики SSL на шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="61328-114">These pre-defined policies can be used to quickly configure an SSL policy on your application gateway.</span></span> <span data-ttu-id="61328-115">Если определенная политика SSL не выбрана, по умолчанию выбирается политика **AppGwSslPolicy20170401**.</span><span class="sxs-lookup"><span data-stu-id="61328-115">By default **AppGwSslPolicy20170401** is selected if no specific SSL policy is defined.</span></span>

<span data-ttu-id="61328-116">Ниже приведен пример выполнения командлета `Get-AzureRmApplicationGatewaySslPredefinedPolicy`.</span><span class="sxs-lookup"><span data-stu-id="61328-116">The following is an example of running `Get-AzureRmApplicationGatewaySslPredefinedPolicy`.</span></span>

```
Name: AppGwSslPolicy20150501
MinProtocolVersion: TLSv1_0
CipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
 ...
Name: AppGwSslPolicy20170401
MinProtocolVersion: TLSv1_1
CipherSuites:
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
...
```

## <a name="configure-a-custom-ssl-policy"></a><span data-ttu-id="61328-117">Настройка пользовательской политики SSL</span><span class="sxs-lookup"><span data-stu-id="61328-117">Configure a custom SSL policy</span></span>

<span data-ttu-id="61328-118">Ниже представлен пример задания пользовательской политики SSL на шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="61328-118">The following example sets a custom SSL policy on an application gateway.</span></span> <span data-ttu-id="61328-119">В качестве минимальной версии протокола она задает версию `TLSv1_1` и включает следующие комплекты шифров.</span><span class="sxs-lookup"><span data-stu-id="61328-119">It sets the minimum protocol version to `TLSv1_1` and enables the following cipher suites:</span></span>

* <span data-ttu-id="61328-120">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="61328-120">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
* <span data-ttu-id="61328-121">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="61328-121">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61328-122">При настройке пользовательской политики SSL необходимо выбрать хотя бы один комплект шифров из следующего списка.</span><span class="sxs-lookup"><span data-stu-id="61328-122">At least one cipher suite from the following list must be selected when configuring a custom SSL policy.</span></span> <span data-ttu-id="61328-123">Для управления серверной частью шлюз приложений использует комплекты шифров RSA SHA256.</span><span class="sxs-lookup"><span data-stu-id="61328-123">Application gateway uses RSA SHA256 cipher suites for backend management.</span></span>
> * <span data-ttu-id="61328-124">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="61328-124">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
> * <span data-ttu-id="61328-125">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="61328-125">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
> * <span data-ttu-id="61328-126">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="61328-126">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="61328-127">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="61328-127">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="61328-128">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="61328-128">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
> * <span data-ttu-id="61328-129">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="61328-129">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

```powershell
# get an application gateway resource
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroup AdatumAppGatewayRG

# set the SSL policy on the application gateway
Set-AzureRmApplicationGatewaySslPolicy -ApplicationGateway $gw -PolicyType Custom -MinProtocolVersion TLSv1_1 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-an-application-gateway-with-a-pre-defined-ssl-policy"></a><span data-ttu-id="61328-130">Создание шлюза приложений со стандартной политикой SSL</span><span class="sxs-lookup"><span data-stu-id="61328-130">Create an application gateway with a pre-defined SSL policy</span></span>

<span data-ttu-id="61328-131">В следующем примере создается шлюз приложений со стандартной политикой SSL.</span><span class="sxs-lookup"><span data-stu-id="61328-131">The following example creates a new application gateway with a pre-defined SSL policy.</span></span>

```powershell
# Create a resource group
$rg = New-AzureRmResourceGroup -Name ContosoRG -Location "East US"
# Create a subnet for the application gateway
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
# Create a virtual network with a 10.0.0.0/16 address space
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName $rg.ResourceGroupName -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
# Retrieve the subnet object for later use
$subnet = $vnet.Subnets[0]
# Create a public IP address
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName $rg.ResourceGroupName -name publicIP01 -location "East US" -AllocationMethod Dynamic
# Create a ip configuration object
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
# Create a backend pool for backend web servers
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
# Define the backend http settings to be used.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
# Create a new port for SSL
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
# Upload an existing pfx certificate for SSL offload
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile C:\folder\contoso.pfx -Password "P@ssw0rd"
# Create a frontend IP configuration for the public IP address
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
# Create a new listener with the certificate, port, and frontend ip.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
# Create a new rule for backend traffic routing
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
# Define the size of the application gateway
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
# Configure the SSL policy to use a different pre-defined policy
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
# Create the application gateway.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName $rg.ResourceGroupName -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

## <a name="next-steps"></a><span data-ttu-id="61328-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61328-132">Next steps</span></span>

<span data-ttu-id="61328-133">Дополнительные сведения о перенаправлении трафика HTTP на конечную точку HTTPS см. в статье [Общие сведения о перенаправлении для шлюза приложений](application-gateway-redirect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61328-133">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) to learn how to redirect HTTP traffic to a HTTPS endpoint.</span></span>