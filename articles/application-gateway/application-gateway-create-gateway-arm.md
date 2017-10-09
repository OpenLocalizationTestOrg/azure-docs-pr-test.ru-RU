---
title: "aaaCreate и управления ими шлюза приложения Azure — PowerShell | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, Настройка, запуск и удалить шлюз приложения Azure с помощью диспетчера ресурсов Azure"
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
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="ad5c4-103">Создание, запуск или удаление шлюза приложений с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="ad5c4-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ad5c4-104">портал Azure</span><span class="sxs-lookup"><span data-stu-id="ad5c4-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="ad5c4-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="ad5c4-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="ad5c4-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad5c4-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="ad5c4-107">Шаблон диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="ad5c4-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="ad5c4-108">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="ad5c4-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="ad5c4-109">Шлюз приложений — это балансировщик нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="ad5c4-110">Он предоставляет отработки отказа и маршрутизации производительности HTTP-запросов между различными серверами, являются ли они на hello облачной или локальной.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="ad5c4-111">Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="ad5c4-112">Полный список поддерживаемых функций toofind посетите [Обзор шлюза приложения](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ad5c4-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="ad5c4-113">В этой статье рассматриваются действия toocreate hello, Настройка, запуск и удалить шлюз приложения.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad5c4-114">Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчер ресурсов и классическом.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-114">Before you work with Azure resources, it is important toounderstand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="ad5c4-115">Внимательно изучите [модели и средства развертывания](../azure-classic-rm.md), прежде чем начинать работать с любыми ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="ad5c4-116">Для просмотра документации hello для различных средств, щелкнув вкладки hello hello верхней части этой статьи.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-116">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="ad5c4-117">В этом документе рассматривается создание шлюза приложений с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="ad5c4-118">классической версии hello toouse go слишком[создать шлюз классического развертывания приложения с помощью PowerShell](application-gateway-create-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="ad5c4-118">toouse hello classic version, go too[Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ad5c4-119">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="ad5c4-119">Before you begin</span></span>

1. <span data-ttu-id="ad5c4-120">Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="ad5c4-121">Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ad5c4-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="ad5c4-122">При наличии существующей виртуальной сети, выберите существующую пустую подсеть или создать подсеть в существующей виртуальной сети для использования исключительно шлюзом приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="ad5c4-123">Невозможно развернуть hello приложения шлюза tooa другую виртуальную сеть чем hello ресурсы предполагается toodeploy за шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-123">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway.</span></span>
1. <span data-ttu-id="ad5c4-124">должен существовать настройки шлюза приложения hello toouse серверы Hello или назначенные их конечных точек, созданных в hello виртуальной сети или с помощью открытого IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-124">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="ad5c4-125">Что такое необходимые toocreate шлюза приложения</span><span class="sxs-lookup"><span data-stu-id="ad5c4-125">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="ad5c4-126">**Внутренний пул сервера:** список hello IP адресов, полных доменных имен или сетевых адаптеров hello внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-126">**Backend server pool:** hello list of IP addresses, FQDNs, or NICs of hello backend servers.</span></span> <span data-ttu-id="ad5c4-127">При использовании IP-адреса, они должны принадлежать либо к подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-127">If IP addresses are used, they should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="ad5c4-128">**Параметры пула внутренних серверов:** каждый пул имеет такие параметры, как порт, протокол и соответствие на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="ad5c4-129">Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="ad5c4-130">**Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-130">**frontend port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="ad5c4-131">Трафик обращений к этому порту и затем получает перенаправленный tooone hello внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-131">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="ad5c4-132">**Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).</span><span class="sxs-lookup"><span data-stu-id="ad5c4-132">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="ad5c4-133">**Правило:** правило hello привязывает hello прослушивателя, hello внутреннего сервера пула и определяет, какой трафик hello внутреннего пула сервера должен быть расширенный toowhen попадании конкретного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-133">**Rule:** hello rule binds hello listener, hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="ad5c4-134">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="ad5c4-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="ad5c4-135">Убедитесь, что используется последняя версия Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-135">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="ad5c4-136">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ad5c4-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="ad5c4-137">Войдите в tooAzure и введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-137">Log in tooAzure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="ad5c4-138">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-138">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="ad5c4-139">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-139">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="ad5c4-140">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="ad5c4-141">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="ad5c4-142">Это расположение используется в качестве расположения по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-142">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="ad5c4-143">Убедитесь, что все команды toocreate, использует шлюз приложений hello таким же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-143">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="ad5c4-144">В приведенном выше примере hello, мы создали группу ресурсов под названием **ContosoRG** и расположение **Восток США**.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-144">In hello example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="ad5c4-145">Если вам требуется пользовательский зонд tooconfigure для шлюза приложения, посетите: [создать шлюз приложений с пользовательской проверки с помощью PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ad5c4-145">If you need tooconfigure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="ad5c4-146">Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad5c4-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-hello-application-gateway-configuration-objects"></a><span data-ttu-id="ad5c4-147">Создание шлюза приложения hello объекты конфигурации</span><span class="sxs-lookup"><span data-stu-id="ad5c4-147">Create hello application gateway configuration objects</span></span>

<span data-ttu-id="ad5c4-148">Необходимо настроить все элементы конфигурации, перед созданием шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-148">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="ad5c4-149">Hello следующие действия создадут hello элементы конфигурации, которые необходимы для ресурса шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-149">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="ad5c4-150">По завершении получить сведения о DNS и виртуальный IP-адрес шлюза приложения hello из hello открытый IP-ресурс toohello вложенного приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-150">When complete, retrieve DNS and VIP details of hello application gateway from hello public IP resource attached toohello application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="ad5c4-151">Удалить шлюз приложения hello</span><span class="sxs-lookup"><span data-stu-id="ad5c4-151">Delete hello application gateway</span></span>

<span data-ttu-id="ad5c4-152">Hello следующий пример удаляет шлюз приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-152">hello following example deletes hello application gateway.</span></span>

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="ad5c4-153">Hello **-принудительно** коммутатор может быть сообщение с подтверждением remove используется toosuppress hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-153">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="ad5c4-154">tooverify, hello службы были удалены, вы можете использовать hello `Get-AzureRmApplicationGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-154">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="ad5c4-155">Этот шаг не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="ad5c4-156">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="ad5c4-156">Get application gateway DNS name</span></span>

<span data-ttu-id="ad5c4-157">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-157">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="ad5c4-158">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="ad5c4-159">tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-159">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="ad5c4-160">toodo сведения, получение шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="ad5c4-161">Это можно сделать с помощью Azure DNS или других поставщиков DNS, при создании записи CNAME, точек toohello [общедоступный IP-адрес](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="ad5c4-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points toohello [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="ad5c4-162">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="ad5c4-163">IP-адрес назначается шлюз приложений toohello при запуске службы hello.</span><span class="sxs-lookup"><span data-stu-id="ad5c4-163">An IP address is assigned toohello application gateway when hello service starts.</span></span>

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

## <a name="delete-all-resources"></a><span data-ttu-id="ad5c4-164">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="ad5c4-164">Delete all resources</span></span>

<span data-ttu-id="ad5c4-165">toodelete все ресурсы, созданные в этой статье завершения hello следующий шаг:</span><span class="sxs-lookup"><span data-stu-id="ad5c4-165">toodelete all resources created in this article, complete hello following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="ad5c4-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad5c4-166">Next steps</span></span>

<span data-ttu-id="ad5c4-167">Если вы хотите tooconfigure разгрузки SSL, посетите: [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="ad5c4-167">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="ad5c4-168">Если вы хотите tooconfigure toouse шлюза приложения с внутренней подсистемы балансировки нагрузки, посетите: [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="ad5c4-168">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="ad5c4-169">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="ad5c4-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="ad5c4-170">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="ad5c4-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="ad5c4-171">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="ad5c4-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
