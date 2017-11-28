---
title: "aaaCreate пользовательской проверки - шлюз приложений Azure — PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate пользовательской проверки для шлюза приложения с помощью PowerShell в диспетчере ресурсов"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="ac2e2-103">Создание пользовательской проверки для шлюза приложений с помощью PowerShell для диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="ac2e2-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac2e2-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ac2e2-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="ac2e2-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="ac2e2-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="ac2e2-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac2e2-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="ac2e2-107">В этой статье добавьте пользовательский зонд tooan существующего приложения шлюза с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="ac2e2-108">Пользовательские зонды полезны для приложений, имеющих страницы проверки работоспособности конкретного или для приложений, которые не предоставляют успешный ответ на веб-приложения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="ac2e2-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ac2e2-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="ac2e2-110">В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ac2e2-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="ac2e2-111">Создание шлюза приложений с пользовательской пробой</span><span class="sxs-lookup"><span data-stu-id="ac2e2-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="ac2e2-112">Вход и создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="ac2e2-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="ac2e2-113">Используйте `Login-AzureRmAccount` tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-113">Use `Login-AzureRmAccount` tooauthenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="ac2e2-114">Получите hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-114">Get hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="ac2e2-115">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-115">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="ac2e2-116">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-116">Create a resource group.</span></span> <span data-ttu-id="ac2e2-117">Если у вас есть группа ресурсов, можно пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="ac2e2-118">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="ac2e2-119">Это расположение используется в качестве расположения по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-119">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="ac2e2-120">Убедитесь, что все команды toocreate hello использование шлюза приложений одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-120">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="ac2e2-121">В предыдущих пример hello, мы создали группу ресурсов под названием **appgw RG** в расположении **Запад США**.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-121">In hello preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="ac2e2-122">Создание виртуальной сети и подсети</span><span class="sxs-lookup"><span data-stu-id="ac2e2-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="ac2e2-123">Hello следующий пример создает виртуальную сеть и подсети для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-123">hello following example creates a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="ac2e2-124">Шлюзу приложений требуется собственная подсеть.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="ac2e2-125">По этой причине hello подсети для шлюза приложения hello должно быть меньше hello адресном пространстве tooallow hello виртуальной сети для других toobe подсети и использовать его.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-125">For this reason, hello subnet created for hello application gateway should be smaller than hello address space of hello VNET tooallow for other subnets toobe created and used.</span></span>

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="ac2e2-126">Создать общедоступный IP-адрес для интерфейса конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="ac2e2-126">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="ac2e2-127">Создание общих ресурсов IP **publicIP01** в группе ресурсов **appgw rg** для региона hello Запад США.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="ac2e2-128">Этот пример использует общедоступный IP-адрес для hello внешнего IP-адреса шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-128">This example uses a public IP address for hello front-end IP address of hello application gateway.</span></span>  <span data-ttu-id="ac2e2-129">Шлюз приложений требует toohave IP адрес hello для открытого динамически созданные DNS-имя, поэтому hello `-DomainNameLabel` не может указываться во время создания hello hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-129">Application gateway requires hello public IP address toohave a dynamically created DNS name therefore hello `-DomainNameLabel` cannot be specified during hello creation of hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="ac2e2-130">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="ac2e2-130">Create an application gateway</span></span>

<span data-ttu-id="ac2e2-131">Настройка всех элементов конфигурации перед созданием шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-131">You set up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="ac2e2-132">Hello следующий пример создает hello элементы конфигурации, которые необходимы для ресурса шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-132">hello following example creates hello configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="ac2e2-133">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="ac2e2-133">**Component**</span></span> | <span data-ttu-id="ac2e2-134">**Описание**</span><span class="sxs-lookup"><span data-stu-id="ac2e2-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="ac2e2-135">**Конфигурация IP-адреса шлюза**</span><span class="sxs-lookup"><span data-stu-id="ac2e2-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="ac2e2-136">Конфигурация IP-адреса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="ac2e2-137">**Внутренний пул**</span><span class="sxs-lookup"><span data-stu-id="ac2e2-137">**Backend pool**</span></span> | <span data-ttu-id="ac2e2-138">Пул IP-адресов, полных доменных ИМЕН и сетевые адаптеры, являются toohello серверы приложений, для размещения веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="ac2e2-138">A pool of IP addresses, FQDN's, or NICs that are toohello application servers that host hello web application</span></span>|
| <span data-ttu-id="ac2e2-139">**Зонд работоспособности**</span><span class="sxs-lookup"><span data-stu-id="ac2e2-139">**Health probe**</span></span> | <span data-ttu-id="ac2e2-140">Пользовательский зонд используется toomonitor hello работоспособности членов пула внутренних hello</span><span class="sxs-lookup"><span data-stu-id="ac2e2-140">A custom probe used toomonitor hello health of hello backend pool members</span></span>|
| <span data-ttu-id="ac2e2-141">**Параметры HTTP**</span><span class="sxs-lookup"><span data-stu-id="ac2e2-141">**HTTP settings**</span></span> | <span data-ttu-id="ac2e2-142">Коллекция параметров, в том числе порта, протокола, сходства на основе файлов cookie, пробы и времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="ac2e2-143">Эти параметры определяют, как трафика — члены пула перенаправленное toohello серверной части</span><span class="sxs-lookup"><span data-stu-id="ac2e2-143">These settings determine how traffic is routed toohello backend pool members</span></span>|
| <span data-ttu-id="ac2e2-144">**Интерфейсный порт**</span><span class="sxs-lookup"><span data-stu-id="ac2e2-144">**Frontend port**</span></span> | <span data-ttu-id="ac2e2-145">порт Hello, hello шлюз приложений прослушивает трафик на</span><span class="sxs-lookup"><span data-stu-id="ac2e2-145">hello port that hello application gateway listens for traffic on</span></span>|
| <span data-ttu-id="ac2e2-146">**Прослушиватель**</span><span class="sxs-lookup"><span data-stu-id="ac2e2-146">**Listener**</span></span> | <span data-ttu-id="ac2e2-147">Сочетание протокола, конфигурации интерфейсного IP-адреса и интерфейсного порта.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="ac2e2-148">Это компонент, который прослушивает входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="ac2e2-149">**Правило**</span><span class="sxs-lookup"><span data-stu-id="ac2e2-149">**Rule**</span></span>| <span data-ttu-id="ac2e2-150">Маршруты hello соответствующих серверных toohello трафика на основе параметров HTTP.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-150">Routes hello traffic toohello appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a><span data-ttu-id="ac2e2-151">Добавление шлюза проверки tooan существующего приложения</span><span class="sxs-lookup"><span data-stu-id="ac2e2-151">Add a probe tooan existing application gateway</span></span>

<span data-ttu-id="ac2e2-152">Hello следующий фрагмент кода добавляет шлюза проверки tooan существующих приложений.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-152">hello following code snippet adds a probe tooan existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="ac2e2-153">Удаление проверки из существующего шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="ac2e2-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="ac2e2-154">Следующий фрагмент кода Hello удаляет зонда из существующего шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-154">hello following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="ac2e2-155">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="ac2e2-155">Get application gateway DNS name</span></span>

<span data-ttu-id="ac2e2-156">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-156">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="ac2e2-157">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="ac2e2-158">tooensure конечным пользователям возможность нажать шлюза приложения hello, можно использовать запись CNAME toopoint toohello общедоступную конечную точку шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-158">tooensure end users can hit hello application gateway a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="ac2e2-159">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ac2e2-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="ac2e2-160">toodo сведения, получение шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="ac2e2-161">шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-161">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="ac2e2-162">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="ac2e2-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="ac2e2-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac2e2-163">Next steps</span></span>

<span data-ttu-id="ac2e2-164">Узнайте, tooconfigure разгрузки SSL, посетив: [Настройка разгрузки SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="ac2e2-164">Learn tooconfigure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

