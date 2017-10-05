---
title: "Создание пользовательской пробы для шлюза приложений Azure с помощью PowerShell | Документация Майкрософт"
description: "Узнайте, как создать пользовательскую проверку для шлюза приложений с помощью PowerShell в диспетчере ресурсов."
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
ms.openlocfilehash: b54fe5267d87a41eb9e81d5d1dc9b1b16c5c5e88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="6f49e-103">Создание пользовательской проверки для шлюза приложений с помощью PowerShell для диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="6f49e-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f49e-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="6f49e-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="6f49e-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="6f49e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="6f49e-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f49e-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="6f49e-107">Следуя инструкциям этой статьи вы добавите пользовательскую пробу в имеющийся шлюз приложений с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f49e-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="6f49e-108">Пользовательские пробы полезны в приложениях с конкретной страницей проверки работоспособности или приложениях, не предоставляющих успешный ответ веб-приложению по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6f49e-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="6f49e-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6f49e-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="6f49e-110">В этой статье описывается использование модели развертывания c помощью Resource Manager. Для большинства новых развертываний мы рекомендуем использовать эту модель вместо [классической](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6f49e-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="6f49e-111">Создание шлюза приложений с пользовательской пробой</span><span class="sxs-lookup"><span data-stu-id="6f49e-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="6f49e-112">Вход и создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="6f49e-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="6f49e-113">Используйте `Login-AzureRmAccount` для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="6f49e-113">Use `Login-AzureRmAccount` to authenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="6f49e-114">Получите подписку для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6f49e-114">Get the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="6f49e-115">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="6f49e-115">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="6f49e-116">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6f49e-116">Create a resource group.</span></span> <span data-ttu-id="6f49e-117">Если у вас есть группа ресурсов, можно пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="6f49e-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="6f49e-118">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="6f49e-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="6f49e-119">Это расположение используется в качестве расположения по умолчанию для всех ресурсов данной группы.</span><span class="sxs-lookup"><span data-stu-id="6f49e-119">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="6f49e-120">Убедитесь, что во всех командах для создания шлюза приложений используется одна группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6f49e-120">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="6f49e-121">В примере выше мы создали группу ресурсов **appgw-RG** в **западной части США**.</span><span class="sxs-lookup"><span data-stu-id="6f49e-121">In the preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="6f49e-122">Создание виртуальной сети и подсети</span><span class="sxs-lookup"><span data-stu-id="6f49e-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="6f49e-123">Следующий пример кода создает виртуальную сеть и подсеть шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6f49e-123">The following example creates a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="6f49e-124">Шлюзу приложений требуется собственная подсеть.</span><span class="sxs-lookup"><span data-stu-id="6f49e-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="6f49e-125">По этой причине созданная для него подсеть должна быть меньше адресного пространства виртуальной сети. Это позволит создавать и использовать другие подсети.</span><span class="sxs-lookup"><span data-stu-id="6f49e-125">For this reason, the subnet created for the application gateway should be smaller than the address space of the VNET to allow for other subnets to be created and used.</span></span>

```powershell
# Assign the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for the next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="6f49e-126">Создание общедоступного IP-адреса для конфигурации интерфейсной части</span><span class="sxs-lookup"><span data-stu-id="6f49e-126">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="6f49e-127">Создайте ресурс общедоступного IP-адреса с именем **publicIP01** в группе ресурсов **appgw-rg** для региона "Западная часть США".</span><span class="sxs-lookup"><span data-stu-id="6f49e-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="6f49e-128">В этом примере для интерфейсных IP-адресов шлюза приложений используются общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="6f49e-128">This example uses a public IP address for the front-end IP address of the application gateway.</span></span>  <span data-ttu-id="6f49e-129">Шлюзу приложений требуется общедоступный IP-адрес с динамически созданным DNS-именем, поэтому при создании общедоступных IP-адресов нельзя указывать `-DomainNameLabel`.</span><span class="sxs-lookup"><span data-stu-id="6f49e-129">Application gateway requires the public IP address to have a dynamically created DNS name therefore the `-DomainNameLabel` cannot be specified during the creation of the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="6f49e-130">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="6f49e-130">Create an application gateway</span></span>

<span data-ttu-id="6f49e-131">Перед созданием шлюза приложений необходимо настроить все элементы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6f49e-131">You set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="6f49e-132">Пример кода ниже создает элементы конфигурации, необходимые для ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6f49e-132">The following example creates the configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="6f49e-133">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="6f49e-133">**Component**</span></span> | <span data-ttu-id="6f49e-134">**Описание**</span><span class="sxs-lookup"><span data-stu-id="6f49e-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="6f49e-135">**Конфигурация IP-адреса шлюза**</span><span class="sxs-lookup"><span data-stu-id="6f49e-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="6f49e-136">Конфигурация IP-адреса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6f49e-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="6f49e-137">**Серверный пул**</span><span class="sxs-lookup"><span data-stu-id="6f49e-137">**Backend pool**</span></span> | <span data-ttu-id="6f49e-138">Пул IP-адресов, полное доменное имя или сетевые адаптеры серверов приложений, на которых размещается веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="6f49e-138">A pool of IP addresses, FQDN's, or NICs that are to the application servers that host the web application</span></span>|
| <span data-ttu-id="6f49e-139">**Проба работоспособности**</span><span class="sxs-lookup"><span data-stu-id="6f49e-139">**Health probe**</span></span> | <span data-ttu-id="6f49e-140">Пользовательская проба, используемая для мониторинга работоспособности участников серверного пула.</span><span class="sxs-lookup"><span data-stu-id="6f49e-140">A custom probe used to monitor the health of the backend pool members</span></span>|
| <span data-ttu-id="6f49e-141">**Параметры HTTP**</span><span class="sxs-lookup"><span data-stu-id="6f49e-141">**HTTP settings**</span></span> | <span data-ttu-id="6f49e-142">Коллекция параметров, в том числе порта, протокола, сходства на основе файлов cookie, пробы и времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="6f49e-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="6f49e-143">Эти параметры определяют передачу трафика участникам серверного пула.</span><span class="sxs-lookup"><span data-stu-id="6f49e-143">These settings determine how traffic is routed to the backend pool members</span></span>|
| <span data-ttu-id="6f49e-144">**Интерфейсный порт**</span><span class="sxs-lookup"><span data-stu-id="6f49e-144">**Frontend port**</span></span> | <span data-ttu-id="6f49e-145">Порт, на котором шлюз приложений прослушивает трафик.</span><span class="sxs-lookup"><span data-stu-id="6f49e-145">The port that the application gateway listens for traffic on</span></span>|
| <span data-ttu-id="6f49e-146">**Прослушиватель**</span><span class="sxs-lookup"><span data-stu-id="6f49e-146">**Listener**</span></span> | <span data-ttu-id="6f49e-147">Сочетание протокола, конфигурации интерфейсного IP-адреса и интерфейсного порта.</span><span class="sxs-lookup"><span data-stu-id="6f49e-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="6f49e-148">Это компонент, который прослушивает входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="6f49e-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="6f49e-149">**Правило**</span><span class="sxs-lookup"><span data-stu-id="6f49e-149">**Rule**</span></span>| <span data-ttu-id="6f49e-150">Направляет трафик в соответствующую серверную часть на основе параметров HTTP.</span><span class="sxs-lookup"><span data-stu-id="6f49e-150">Routes the traffic to the appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates the backend http settings to be used. This component references the $probe created in the previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for the application gateway to listen on port 80 that will be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates the $publicip variable defined previously with the front-end IP that will be used by the listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates the listener. The listener is a combination of protocol and the frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates the rule that routes traffic to the backend pools.  In this example we create a basic rule that uses the previous defined http settings and backend address pool.  It also associates the listener to the rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets the SKU of the application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# The final step creates the application gateway with all the previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-to-an-existing-application-gateway"></a><span data-ttu-id="6f49e-151">Добавление проверки для существующего шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="6f49e-151">Add a probe to an existing application gateway</span></span>

<span data-ttu-id="6f49e-152">Следующий фрагмент кода добавляет пробу в имеющийся шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="6f49e-152">The following code snippet adds a probe to an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create the probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set the backend HTTP settings to use the new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="6f49e-153">Удаление проверки из существующего шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="6f49e-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="6f49e-154">Следующий фрагмент кода удаляет пробу из имеющегося шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6f49e-154">The following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove the probe from the application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set the backend HTTP settings to remove the reference to the probe. The backend http settings now use the default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="6f49e-155">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="6f49e-155">Get application gateway DNS name</span></span>

<span data-ttu-id="6f49e-156">После создания шлюза следует настроить внешний интерфейс для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="6f49e-156">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="6f49e-157">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="6f49e-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="6f49e-158">Чтобы гарантировать попадание пользователей на шлюз приложений, можно использовать запись CNAME, чтобы указать общедоступную конечную точку шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="6f49e-158">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="6f49e-159">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6f49e-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="6f49e-160">Получите информацию о шлюзе приложений и соответствующее IP- или DNS-имя с помощью элемента PublicIPAddress, связанного со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="6f49e-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="6f49e-161">DNS-имя шлюза приложений должно использоваться для создания записи CNAME, указывающей двум веб-приложениям на это DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="6f49e-161">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="6f49e-162">Использование записи A не рекомендуется, так как виртуальный IP-адрес может измениться после перезапуска приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="6f49e-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6f49e-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f49e-163">Next steps</span></span>

<span data-ttu-id="6f49e-164">Сведения о настройке разгрузки SSL см. в статье [Настройка шлюза приложений для разгрузки SSL с помощью диспетчера ресурсов Azure](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="6f49e-164">Learn to configure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

