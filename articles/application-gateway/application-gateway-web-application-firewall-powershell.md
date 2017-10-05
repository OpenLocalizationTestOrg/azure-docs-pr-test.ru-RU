---
title: "Настройка брандмауэра веб-приложения для шлюза приложений Azure | Документация Майкрософт"
description: "Эта статья содержит рекомендации о том, как приступить к работе с брандмауэром веб-приложения на существующем или новом шлюзе приложений."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="4691e-103">Настройка брандмауэра веб-приложения на новом или существующем шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="4691e-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4691e-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="4691e-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="4691e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4691e-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="4691e-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="4691e-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="4691e-107">Узнайте, как создать шлюз приложений с брандмауэром веб-приложения или добавить брандмауэр веб-приложения в существующий шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="4691e-107">Learn how to create a web application firewall enabled Application Gateway or add web application firewall to an existing Application Gateway.</span></span>

<span data-ttu-id="4691e-108">Брандмауэр веб-приложения (WAF) в шлюзе приложений Azure защищает веб-приложения от таких распространенных сетевых атак, как атаки путем внедрения кода SQL, атаки межсайтовых сценариев и захваты сеанса.</span><span class="sxs-lookup"><span data-stu-id="4691e-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="4691e-109">Шлюз приложений — это балансировщик нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="4691e-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="4691e-110">Он отвечает за отработку отказов и эффективную маршрутизацию HTTP-запросов между разными серверами (облачными и локальными).</span><span class="sxs-lookup"><span data-stu-id="4691e-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="4691e-111">Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д.</span><span class="sxs-lookup"><span data-stu-id="4691e-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="4691e-112">Полный список поддерживаемых функций представлен в [обзоре шлюза приложений](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4691e-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="4691e-113">В следующей статье рассказывается, как [добавить брандмауэр веб-приложения в существующий шлюз приложений](#add-web-application-firewall-to-an-existing-application-gateway) и как [создать шлюз приложений с брандмауэром веб-приложения](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="4691e-113">The following article shows how to [add web application firewall to an existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![Изображение для сценария][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="4691e-115">Различия в конфигурации WAF</span><span class="sxs-lookup"><span data-stu-id="4691e-115">WAF configuration differences</span></span>

<span data-ttu-id="4691e-116">Если вы прочитали раздел [Создание шлюза приложений с помощью PowerShell](application-gateway-create-gateway-arm.md), то уже понимаете, какие параметры SKU нужно настроить при создании шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="4691e-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an Application Gateway.</span></span> <span data-ttu-id="4691e-117">При настройке SKU для шлюза приложений доступны дополнительные параметры, относящиеся к WAF.</span><span class="sxs-lookup"><span data-stu-id="4691e-117">WAF provides additional settings to define when configuring the SKU on an Application Gateway.</span></span> <span data-ttu-id="4691e-118">Какие-либо изменения самого шлюза приложений не требуются.</span><span class="sxs-lookup"><span data-stu-id="4691e-118">There are no additional changes that you make on the Application Gateway itself.</span></span>

| <span data-ttu-id="4691e-119">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="4691e-119">**Setting**</span></span> | <span data-ttu-id="4691e-120">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="4691e-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="4691e-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="4691e-121">**SKU**</span></span> |<span data-ttu-id="4691e-122">Обычный шлюз приложений без WAF поддерживает размеры **Standard\_Small**, **Standard\_Medium** и **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="4691e-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="4691e-123">После добавления WAF становятся доступны еще два SKU, **WAF\_Medium** и **WAF\_Large**.</span><span class="sxs-lookup"><span data-stu-id="4691e-123">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="4691e-124">WAF не поддерживается в шлюзах приложения уровня "Мелкий".</span><span class="sxs-lookup"><span data-stu-id="4691e-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="4691e-125">**Уровень**</span><span class="sxs-lookup"><span data-stu-id="4691e-125">**Tier**</span></span> | <span data-ttu-id="4691e-126">Доступные значения: **Стандартный** или **WAF**.</span><span class="sxs-lookup"><span data-stu-id="4691e-126">The available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="4691e-127">При использовании брандмауэра веб-приложения требуется выбрать уровень **WAF**.</span><span class="sxs-lookup"><span data-stu-id="4691e-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="4691e-128">**Режим**</span><span class="sxs-lookup"><span data-stu-id="4691e-128">**Mode**</span></span> | <span data-ttu-id="4691e-129">Этот параметр определяет режим WAF.</span><span class="sxs-lookup"><span data-stu-id="4691e-129">This setting is the mode of WAF.</span></span> <span data-ttu-id="4691e-130">Допустимые значения: **Обнаружение** и **Предотвращение**.</span><span class="sxs-lookup"><span data-stu-id="4691e-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="4691e-131">Если WAF работает в режиме обнаружения, все угрозы заносятся в файл журнала.</span><span class="sxs-lookup"><span data-stu-id="4691e-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="4691e-132">В режиме предотвращения события по-прежнему регистрируются в журнале, но злоумышленник получает от шлюза приложений ответ "403 — не авторизовано".</span><span class="sxs-lookup"><span data-stu-id="4691e-132">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the Application Gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="4691e-133">Добавление брандмауэра веб-приложения в существующий шлюз приложений</span><span class="sxs-lookup"><span data-stu-id="4691e-133">Add web application firewall to an existing Application Gateway</span></span>

<span data-ttu-id="4691e-134">Убедитесь, что у вас установлена последняя версия Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4691e-134">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="4691e-135">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4691e-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="4691e-136">Войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="4691e-136">Log in to your Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="4691e-137">Выберите подписку для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="4691e-137">Select the subscription to use for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="4691e-138">Получите шлюз, в который следует добавить брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4691e-138">Retrieve the gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="4691e-139">Настройте SKU брандмауэра веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4691e-139">Configure the web application firewall sku.</span></span> <span data-ttu-id="4691e-140">Доступные размеры: **WAF\_Large** и **WAF\_Medium**.</span><span class="sxs-lookup"><span data-stu-id="4691e-140">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="4691e-141">Для использования брандмауэра веб-приложения требуется уровень **WAF**, а емкость необходимо подтвердить при определении SKU.</span><span class="sxs-lookup"><span data-stu-id="4691e-141">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="4691e-142">Настройте параметры WAF, как указано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="4691e-142">Configure the WAF settings as defined in the following example:</span></span>

   <span data-ttu-id="4691e-143">Для параметра **FirewallMode** можно указать значение "Обнаружение" или "Предотвращение".</span><span class="sxs-lookup"><span data-stu-id="4691e-143">For **FirewallMode**, the available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="4691e-144">Примените к шлюзу приложений параметры, определенные на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="4691e-144">Update the Application Gateway with the settings defined in the preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="4691e-145">Эта команда обновляет шлюз приложений, добавляя в него брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4691e-145">This command updates the Application Gateway with web application firewall.</span></span> <span data-ttu-id="4691e-146">Ознакомьтесь с [диагностикой шлюза приложений](application-gateway-diagnostics.md), чтобы понять, как просматривать журналы шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="4691e-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your Application Gateway.</span></span> <span data-ttu-id="4691e-147">Из-за особенностей системы безопасности WAF необходимо регулярно просматривать журналы, чтобы понимать состояние безопасности веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="4691e-147">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="4691e-148">Создание шлюза приложений с брандмауэром веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4691e-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="4691e-149">Ниже полностью описывается процесс создания шлюза приложений с брандмауэром веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4691e-149">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="4691e-150">Убедитесь, что у вас установлена последняя версия Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4691e-150">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="4691e-151">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4691e-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="4691e-152">Войдите в Azure, выполнив `Login-AzureRmAccount`. Вам будет предложено указать свои учетные данные для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4691e-152">Log in to Azure by running `Login-AzureRmAccount`, you are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="4691e-153">Просмотрите подписки учетной записи, выполнив `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="4691e-153">Check the subscriptions for the account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="4691e-154">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="4691e-154">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="4691e-155">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="4691e-155">Create a resource group</span></span>

<span data-ttu-id="4691e-156">Создайте группу ресурсов для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="4691e-156">Create a resource group for the Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="4691e-157">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="4691e-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="4691e-158">Это расположение используется в качестве расположения по умолчанию для всех ресурсов данной группы.</span><span class="sxs-lookup"><span data-stu-id="4691e-158">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="4691e-159">Убедитесь, что во всех командах для создания шлюза приложений используется одна группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4691e-159">Make sure that all commands to create an Application Gateway uses the same resource group.</span></span>

<span data-ttu-id="4691e-160">В приведенном выше примере мы создали группу ресурсов appgw-RG в расположении West US (западная часть США).</span><span class="sxs-lookup"><span data-stu-id="4691e-160">In the preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="4691e-161">Если вам нужно настроить пользовательскую пробу для шлюза приложений, ознакомьтесь со статьей [Создание пользовательской проверки для шлюза приложений с помощью PowerShell для диспетчера ресурсов Azure](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4691e-161">If you need to configure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="4691e-162">Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4691e-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="4691e-163">Настройка виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="4691e-163">Configure virtual network</span></span>

<span data-ttu-id="4691e-164">Шлюзу приложений требуется собственная подсеть.</span><span class="sxs-lookup"><span data-stu-id="4691e-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="4691e-165">На этом шаге создается виртуальная сеть с адресным пространством 10.0.0.0/16 и две подсети: одна для шлюза приложений и одна для членов внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="4691e-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for the Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="4691e-166">Настройка диапазонов общедоступных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="4691e-166">Configure public IP address</span></span>

<span data-ttu-id="4691e-167">Для обработки внешних запросов шлюзу приложений требуется общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="4691e-167">In order to handle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="4691e-168">Этот общедоступный IP-адрес не должен иметь определений `DomainNameLabel` для использования шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="4691e-168">This public IP address must not have a `DomainNameLabel` defined to be used by the Application Gateway.</span></span>

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a><span data-ttu-id="4691e-169">Настройка шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="4691e-169">Configure the Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="4691e-170">Для защиты шлюзов приложений, созданных с помощью базовой конфигурации брандмауэра веб-приложения, настраивается CRS 3.0.</span><span class="sxs-lookup"><span data-stu-id="4691e-170">Application Gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="4691e-171">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="4691e-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="4691e-172">После создания шлюза следует настроить внешний интерфейс для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="4691e-172">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="4691e-173">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="4691e-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="4691e-174">Чтобы гарантировать попадание пользователей на шлюз приложений, можно использовать запись CNAME, чтобы указать общедоступную конечную точку шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="4691e-174">To ensure end users can hit the Application Gateway, a CNAME record can be used to point to the public endpoint of the Application Gateway.</span></span> <span data-ttu-id="4691e-175">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4691e-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="4691e-176">Чтобы настроить псевдоним, извлеките подробные сведения о шлюзе приложений и соответствующий IP-адрес или DNS-имя с помощью элемента PublicIPAddress, связанного со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="4691e-176">To configure an alias, retrieve details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element attached to the Application Gateway.</span></span> <span data-ttu-id="4691e-177">DNS-имя шлюза приложений должно использоваться для создания записи CNAME, указывающей двум веб-приложениям на это DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="4691e-177">The Application Gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="4691e-178">Использование записи A не рекомендуется, так как виртуальный IP-адрес может измениться после перезапуска шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="4691e-178">The use of A-records is not recommended since the VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4691e-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4691e-179">Next steps</span></span>

<span data-ttu-id="4691e-180">Узнайте, как настроить ведение журнала диагностики и как регистрировать в журнале события, которые обнаружил или предотвратил брандмауэр веб-приложения, посетив страницу [Мониторинг работоспособности серверной части, ведение журнала диагностики и метрики для шлюза приложений](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="4691e-180">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
