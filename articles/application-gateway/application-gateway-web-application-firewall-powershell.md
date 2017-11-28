---
title: "брандмауэр веб-приложения aaaConfigure - шлюз приложений Azure | Документы Microsoft"
description: "Это статье предоставлены рекомендации по как с помощью toostart веб-приложение брандмауэра на шлюза существующего или нового приложения."
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
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="0abda-103">Настройка брандмауэра веб-приложения на новом или существующем шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="0abda-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0abda-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="0abda-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="0abda-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0abda-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="0abda-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="0abda-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="0abda-107">Узнайте, как toocreate брандмауэр веб-приложения включено использование шлюза приложений или добавьте web приложение брандмауэра tooan существующий шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0abda-107">Learn how toocreate a web application firewall enabled Application Gateway or add web application firewall tooan existing Application Gateway.</span></span>

<span data-ttu-id="0abda-108">Hello брандмауэр веб-приложения (WAF) в шлюз приложений Azure защищает веб-приложений из распространенных веб-атак, например путем внедрения кода SQL, атак с использованием межсайтовых сценариев и сеанса захвата.</span><span class="sxs-lookup"><span data-stu-id="0abda-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="0abda-109">Шлюз приложений — это балансировщик нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="0abda-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="0abda-110">Он обеспечивает отработку отказа, маршрутизации производительности HTTP-запросы между различными серверами, являются ли они на hello облачной или локальной.</span><span class="sxs-lookup"><span data-stu-id="0abda-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="0abda-111">Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д.</span><span class="sxs-lookup"><span data-stu-id="0abda-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="0abda-112">Полный список поддерживаемых функций toofind посетите: [шлюза Обзор приложений](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0abda-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="0abda-113">Hello следующей статье показано, каким образом слишком[Добавить web приложение брандмауэра tooan существующий шлюз приложений](#add-web-application-firewall-to-an-existing-application-gateway) и [создания шлюза приложения, использующего брандмауэр веб-приложения](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="0abda-113">hello following article shows how too[add web application firewall tooan existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![Изображение для сценария][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="0abda-115">Различия в конфигурации WAF</span><span class="sxs-lookup"><span data-stu-id="0abda-115">WAF configuration differences</span></span>

<span data-ttu-id="0abda-116">Если вы прочитали [Создание шлюза приложения с помощью PowerShell](application-gateway-create-gateway-arm.md), при создании шлюза приложения, понять tooconfigure параметры hello SKU.</span><span class="sxs-lookup"><span data-stu-id="0abda-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand hello SKU settings tooconfigure when creating an Application Gateway.</span></span> <span data-ttu-id="0abda-117">WAF предоставляет дополнительные параметры toodefine при настройке hello SKU для шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="0abda-117">WAF provides additional settings toodefine when configuring hello SKU on an Application Gateway.</span></span> <span data-ttu-id="0abda-118">Отсутствуют дополнительные изменения, внесенные на сам шлюз приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0abda-118">There are no additional changes that you make on hello Application Gateway itself.</span></span>

| <span data-ttu-id="0abda-119">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="0abda-119">**Setting**</span></span> | <span data-ttu-id="0abda-120">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="0abda-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="0abda-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="0abda-121">**SKU**</span></span> |<span data-ttu-id="0abda-122">Обычный шлюз приложений без WAF поддерживает размеры **Standard\_Small**, **Standard\_Medium** и **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="0abda-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="0abda-123">С появлением hello WAF, приведены два дополнительных конфигураций, **WAF\_Средний** и **WAF\_большой**.</span><span class="sxs-lookup"><span data-stu-id="0abda-123">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="0abda-124">WAF не поддерживается в шлюзах приложения уровня "Мелкий".</span><span class="sxs-lookup"><span data-stu-id="0abda-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="0abda-125">**Уровень**</span><span class="sxs-lookup"><span data-stu-id="0abda-125">**Tier**</span></span> | <span data-ttu-id="0abda-126">Доступные значения Hello: **Стандартная** или **WAF**.</span><span class="sxs-lookup"><span data-stu-id="0abda-126">hello available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="0abda-127">При использовании брандмауэра веб-приложения требуется выбрать уровень **WAF**.</span><span class="sxs-lookup"><span data-stu-id="0abda-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="0abda-128">**Режим**</span><span class="sxs-lookup"><span data-stu-id="0abda-128">**Mode**</span></span> | <span data-ttu-id="0abda-129">Этот параметр является режимом hello WAF.</span><span class="sxs-lookup"><span data-stu-id="0abda-129">This setting is hello mode of WAF.</span></span> <span data-ttu-id="0abda-130">Допустимые значения: **Обнаружение** и **Предотвращение**.</span><span class="sxs-lookup"><span data-stu-id="0abda-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="0abda-131">Если WAF работает в режиме обнаружения, все угрозы заносятся в файл журнала.</span><span class="sxs-lookup"><span data-stu-id="0abda-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="0abda-132">В режиме защиты от по-прежнему регистрируются события, но hello злоумышленник получит 403 несанкционированного ответ от hello шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0abda-132">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello Application Gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="0abda-133">Добавить web приложение брандмауэра tooan существующего шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="0abda-133">Add web application firewall tooan existing Application Gateway</span></span>

<span data-ttu-id="0abda-134">Убедитесь, что используется последняя версия Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0abda-134">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="0abda-135">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0abda-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="0abda-136">Войдите в учетную запись Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="0abda-136">Log in tooyour Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="0abda-137">Выберите toouse hello подписку для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="0abda-137">Select hello subscription toouse for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="0abda-138">Получить hello шлюза, который вы добавляете брандмауэр веб-приложения для.</span><span class="sxs-lookup"><span data-stu-id="0abda-138">Retrieve hello gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="0abda-139">Настройте приложение брандмауэра hello web sku.</span><span class="sxs-lookup"><span data-stu-id="0abda-139">Configure hello web application firewall sku.</span></span> <span data-ttu-id="0abda-140">Доступные размеры Hello **WAF\_большой** и **WAF\_Средний**.</span><span class="sxs-lookup"><span data-stu-id="0abda-140">hello available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="0abda-141">Если используется брандмауэр веб-приложения hello уровня должен быть **WAF**, необходимо подтвердить hello емкости при задании номера sku hello.</span><span class="sxs-lookup"><span data-stu-id="0abda-141">When web application firewall is used hello tier must be **WAF**, hello capacity must be confirmed when setting hello sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="0abda-142">Настройте параметры hello WAF, как определено в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="0abda-142">Configure hello WAF settings as defined in hello following example:</span></span>

   <span data-ttu-id="0abda-143">Для **FirewallMode**, hello доступные значения: Предотвращение и обнаружения.</span><span class="sxs-lookup"><span data-stu-id="0abda-143">For **FirewallMode**, hello available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="0abda-144">Замена hello шлюза приложения hello параметры, определенные в предыдущих шага hello.</span><span class="sxs-lookup"><span data-stu-id="0abda-144">Update hello Application Gateway with hello settings defined in hello preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="0abda-145">Эта команда обновляет hello шлюз приложений брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0abda-145">This command updates hello Application Gateway with web application firewall.</span></span> <span data-ttu-id="0abda-146">Посетите [диагностику шлюза приложения](application-gateway-diagnostics.md) toounderstand как tooview журналы для шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="0abda-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your Application Gateway.</span></span> <span data-ttu-id="0abda-147">Из-за особенностей безопасности toohello WAF toobe необходимость журналы регулярно контролировать состояние безопасности hello toounderstand веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="0abda-147">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="0abda-148">Создание шлюза приложений с брандмауэром веб-приложения</span><span class="sxs-lookup"><span data-stu-id="0abda-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="0abda-149">Hello следующие шаги помогут выполнить весь процесс hello из начала tooend для создания шлюза приложения с помощью брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0abda-149">hello following steps take you through hello entire process from beginning tooend for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="0abda-150">Убедитесь, что используется последняя версия Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0abda-150">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="0abda-151">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0abda-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="0abda-152">Войдите в tooAzure, запустив `Login-AzureRmAccount`, являются tooauthenticate запрос с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="0abda-152">Log in tooAzure by running `Login-AzureRmAccount`, you are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="0abda-153">Проверьте hello подписки для учетной записи hello, выполнив команду`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="0abda-153">Check hello subscriptions for hello account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="0abda-154">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="0abda-154">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="0abda-155">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="0abda-155">Create a resource group</span></span>

<span data-ttu-id="0abda-156">Создание группы ресурсов для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0abda-156">Create a resource group for hello Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="0abda-157">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="0abda-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="0abda-158">Это расположение используется в качестве расположения по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0abda-158">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="0abda-159">Убедитесь, что все команды, которые использует toocreate объект шлюза приложения hello одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0abda-159">Make sure that all commands toocreate an Application Gateway uses hello same resource group.</span></span>

<span data-ttu-id="0abda-160">В предыдущих пример hello мы создали группу ресурсов под названием «Appgw RG» и расположение «Западная часть США.»</span><span class="sxs-lookup"><span data-stu-id="0abda-160">In hello preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="0abda-161">Если вам требуется пользовательский зонд tooconfigure шлюза приложения, см. раздел [создать шлюз приложений с пользовательской проверки с помощью PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0abda-161">If you need tooconfigure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="0abda-162">Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0abda-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="0abda-163">Настройка виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="0abda-163">Configure virtual network</span></span>

<span data-ttu-id="0abda-164">Шлюзу приложений требуется собственная подсеть.</span><span class="sxs-lookup"><span data-stu-id="0abda-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="0abda-165">На этом шаге создается виртуальная сеть с адресным пространством 10.0.0.0/16 и две подсети: для шлюза приложения hello и для внутренних членов пула.</span><span class="sxs-lookup"><span data-stu-id="0abda-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for hello Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="0abda-166">Настройка диапазонов общедоступных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="0abda-166">Configure public IP address</span></span>

<span data-ttu-id="0abda-167">В порядке toohandle внешние запросы шлюз приложений требуется общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0abda-167">In order toohandle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="0abda-168">Этот общедоступный IP-адрес не должен иметь `DomainNameLabel` определенные toobe используемые hello шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0abda-168">This public IP address must not have a `DomainNameLabel` defined toobe used by hello Application Gateway.</span></span>

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a><span data-ttu-id="0abda-169">Настройка шлюза приложения hello</span><span class="sxs-lookup"><span data-stu-id="0abda-169">Configure hello Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="0abda-170">Шлюзы приложений, созданных с помощью конфигурации брандмауэра hello основные веб-приложений, настроенных с CRS 3.0 для защиты.</span><span class="sxs-lookup"><span data-stu-id="0abda-170">Application Gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="0abda-171">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="0abda-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="0abda-172">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="0abda-172">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="0abda-173">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="0abda-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="0abda-174">tooensure конечным пользователям возможность нажать hello шлюза приложения, запись CNAME может быть используется toopoint toohello общедоступная конечная точка hello шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0abda-174">tooensure end users can hit hello Application Gateway, a CNAME record can be used toopoint toohello public endpoint of hello Application Gateway.</span></span> <span data-ttu-id="0abda-175">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0abda-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="0abda-176">tooconfigure псевдоним, получить сведения о hello шлюз приложений и соответствующее IP или DNS-имя с помощью hello PublicIPAddress вложен toohello шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0abda-176">tooconfigure an alias, retrieve details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello Application Gateway.</span></span> <span data-ttu-id="0abda-177">Шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="0abda-177">hello Application Gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="0abda-178">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0abda-178">hello use of A-records is not recommended since hello VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0abda-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0abda-179">Next steps</span></span>

<span data-ttu-id="0abda-180">Узнайте, как ведение журнала диагностики tooconfigure, toolog hello события, которые обнаружены или предотвратить брандмауэр веб-приложения, посетив [диагностики шлюза приложений](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="0abda-180">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
