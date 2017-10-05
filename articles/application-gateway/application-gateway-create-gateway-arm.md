---
title: "Создание и администрирование шлюза приложений Azure с помощью PowerShell | Документация Майкрософт"
description: "На этой странице приводятся инструкции по созданию, настройке, запуску и удалению шлюза приложений Azure с помощью диспетчера ресурсов Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 5f1713365406764998de505ff62309bab9fa2567
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="a1412-103">Создание, запуск или удаление шлюза приложений с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="a1412-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1412-104">портал Azure</span><span class="sxs-lookup"><span data-stu-id="a1412-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="a1412-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="a1412-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="a1412-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1412-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="a1412-107">Шаблон диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="a1412-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="a1412-108">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="a1412-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="a1412-109">Шлюз приложений — это балансировщик нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="a1412-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="a1412-110">Он отвечает за отработку отказов и эффективную маршрутизацию HTTP-запросов между разными серверами (облачными и локальными).</span><span class="sxs-lookup"><span data-stu-id="a1412-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="a1412-111">Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д.</span><span class="sxs-lookup"><span data-stu-id="a1412-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="a1412-112">Полный список поддерживаемых функций представлен в [обзоре шлюза приложений](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a1412-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="a1412-113">В этой статье рассказывается, как создавать, настраивать, запускать и удалять шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="a1412-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1412-114">Прежде чем приступить к работе с ресурсами Azure, обратите внимание на то, что в настоящее время в Azure существует две модели развертывания: классическая модель развертывания и модель Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a1412-114">Before you work with Azure resources, it is important to understand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="a1412-115">Внимательно изучите [модели и средства развертывания](../azure-classic-rm.md), прежде чем начинать работать с любыми ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="a1412-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="a1412-116">Для просмотра документации о средствах развертывания выбирайте соответствующие вкладки в верхней части данной статьи.</span><span class="sxs-lookup"><span data-stu-id="a1412-116">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="a1412-117">В этом документе рассматривается создание шлюза приложений с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a1412-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="a1412-118">Сведения об использовании классической модели развертывания см. в статье [Создание, запуск или удаление шлюза приложений](application-gateway-create-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="a1412-118">To use the classic version, go to [Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a1412-119">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a1412-119">Before you begin</span></span>

1. <span data-ttu-id="a1412-120">Установите последнюю версию командлетов Azure PowerShell, используя установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="a1412-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="a1412-121">Вы можете скачать и установить последнюю версию из раздела **Windows PowerShell** на [странице загрузок](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a1412-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="a1412-122">Если у вас есть виртуальная сеть, выберите в ней пустую подсеть или создайте другую подсеть для использования только шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="a1412-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="a1412-123">Шлюз приложений можно развернуть только в той виртуальной сети, где находятся ресурсы, которые нужно развернуть на базе шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1412-123">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway.</span></span>
1. <span data-ttu-id="a1412-124">Для использования шлюза приложений настраиваются существующие серверы или серверы, для которых в виртуальной сети созданы конечные точки либо же назначен общедоступный или виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a1412-124">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="a1412-125">Что необходимо для создания шлюза приложений?</span><span class="sxs-lookup"><span data-stu-id="a1412-125">What is required to create an application gateway?</span></span>

* <span data-ttu-id="a1412-126">**Внутренний пул серверов.** Список IP-адресов, полных доменных имен или сетевых адаптеров внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="a1412-126">**Backend server pool:** The list of IP addresses, FQDNs, or NICs of the backend servers.</span></span> <span data-ttu-id="a1412-127">Если используются IP-адреса, они должны относиться к подсети виртуальной сети либо представлять собой общедоступные или виртуальные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="a1412-127">If IP addresses are used, they should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="a1412-128">**Параметры пула внутренних серверов:** каждый пул имеет такие параметры, как порт, протокол и соответствие на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="a1412-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="a1412-129">Эти параметры привязываются к пулу и применяются ко всем серверам в этом пуле.</span><span class="sxs-lookup"><span data-stu-id="a1412-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="a1412-130">**Интерфейсный порт**. Общедоступный порт, открытый в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="a1412-130">**frontend port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="a1412-131">Трафик поступает в этот порт, а затем перенаправляется на один из внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="a1412-131">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="a1412-132">**Прослушиватель**. У прослушивателя есть интерфейсный порт, протокол (Http или Https — с учетом регистра) и имя SSL-сертификата (в случае настройки разгрузки SSL).</span><span class="sxs-lookup"><span data-stu-id="a1412-132">**Listener:** The listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="a1412-133">**Правило.** Правило связывает прослушиватель и пул внутренних серверов и определяет, в какой пул внутренних серверов должен направляться трафик, попадающий в определенный прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="a1412-133">**Rule:** The rule binds the listener, the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="a1412-134">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="a1412-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="a1412-135">Убедитесь, что у вас установлена последняя версия Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1412-135">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="a1412-136">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a1412-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="a1412-137">Войдите в Azure и введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="a1412-137">Log in to Azure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="a1412-138">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a1412-138">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="a1412-139">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="a1412-139">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="a1412-140">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="a1412-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="a1412-141">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="a1412-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="a1412-142">Это расположение используется в качестве расположения по умолчанию для всех ресурсов данной группы.</span><span class="sxs-lookup"><span data-stu-id="a1412-142">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="a1412-143">Убедитесь, что во всех командах для создания шлюза приложений используется одна группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a1412-143">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="a1412-144">В приведенном выше примере мы создали группу ресурсов **ContosoRG** в регионе **восточная часть США**.</span><span class="sxs-lookup"><span data-stu-id="a1412-144">In the example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="a1412-145">Если вам нужно настроить пользовательскую пробу для шлюза приложений, ознакомьтесь со статьей [Создание пользовательской проверки для шлюза приложений с помощью PowerShell для Azure Resource Manager](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a1412-145">If you need to configure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="a1412-146">Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1412-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-the-application-gateway-configuration-objects"></a><span data-ttu-id="a1412-147">Создание объекта конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a1412-147">Create the application gateway configuration objects</span></span>

<span data-ttu-id="a1412-148">Перед созданием шлюза приложений необходимо настроить все элементы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a1412-148">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="a1412-149">В ходе следующих шагов создаются необходимые элементы конфигурации для ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1412-149">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign the address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with the address space of 10.0.0.0/16 and add the subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve the newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used to connect to the application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. The gateway picks up an IP addressfrom the configured subnet and routes network traffic to the IP addresses in the backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with the addresses of your web servers. These backend pool members are all validated to be healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed to them when requests come into the application gateway. Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings to determine the protocol and port that is used when sending traffic to the backend servers. Cookie-based sessions are also determined by the backend HTTP settings.  If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used to connect to the application gateway through the public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure the frontend IP configuration with the public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure the listener.  The listener is a combination of the front end IP configuration, protocol, and port and is used to receive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used to route traffic to the backend servers. The backend pool settings, listener, and backend pool created in the previous steps make up the rule. Based on the criteria defined traffic is routed to the appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU for the application gateway, this determines the size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create the application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="a1412-150">По завершении извлеките сведения о виртуальном IP-адресе и сервере DNS шлюза приложений из ресурса с общедоступным IP-адресом, присоединенного к этому шлюзу.</span><span class="sxs-lookup"><span data-stu-id="a1412-150">When complete, retrieve DNS and VIP details of the application gateway from the public IP resource attached to the application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="a1412-151">Удаление шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a1412-151">Delete the application gateway</span></span>

<span data-ttu-id="a1412-152">В следующем примере удаляется шлюз приложения.</span><span class="sxs-lookup"><span data-stu-id="a1412-152">The following example deletes the application gateway.</span></span>

```powershell
# Retrieve the application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops the application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="a1412-153">Если указать параметр **-force**, запрос на подтверждение удаления не появится.</span><span class="sxs-lookup"><span data-stu-id="a1412-153">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="a1412-154">Для проверки того, удалена ли служба, используйте командлет `Get-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="a1412-154">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="a1412-155">Этот шаг не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="a1412-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="a1412-156">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a1412-156">Get application gateway DNS name</span></span>

<span data-ttu-id="a1412-157">После создания шлюза следует настроить внешний интерфейс для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="a1412-157">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="a1412-158">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="a1412-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="a1412-159">Чтобы гарантировать попадание пользователей на шлюз приложений, можно использовать запись CNAME, чтобы указать общедоступную конечную точку шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1412-159">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="a1412-160">Получите информацию о шлюзе приложений и соответствующее IP- или DNS-имя с помощью элемента PublicIPAddress, связанного со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="a1412-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="a1412-161">Это можно сделать с помощью Azure DNS или других поставщиков DNS, создав запись CNAME, которая указывает на [общедоступный IP-адрес](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="a1412-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points to the [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="a1412-162">Использование записи A не рекомендуется, так как виртуальный IP-адрес может измениться после перезапуска приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="a1412-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="a1412-163">IP-адрес назначается шлюзу приложений при запуске службы.</span><span class="sxs-lookup"><span data-stu-id="a1412-163">An IP address is assigned to the application gateway when the service starts.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
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

## <a name="delete-all-resources"></a><span data-ttu-id="a1412-164">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="a1412-164">Delete all resources</span></span>

<span data-ttu-id="a1412-165">Чтобы удалить все ресурсы, созданные в этой статье, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a1412-165">To delete all resources created in this article, complete the following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="a1412-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1412-166">Next steps</span></span>

<span data-ttu-id="a1412-167">Чтобы настроить разгрузку SSL, ознакомьтесь с [настройкой шлюза приложений для разгрузки SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="a1412-167">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="a1412-168">Указания по настройке шлюза приложений для использования с внутренним балансировщиком нагрузки см. в статье [Создание шлюза приложений с внутренней подсистемой балансировщика нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="a1412-168">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="a1412-169">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="a1412-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="a1412-170">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="a1412-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="a1412-171">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="a1412-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
