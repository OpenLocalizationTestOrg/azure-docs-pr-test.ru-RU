---
title: "aaaConfigure SSL разгрузки - шлюз приложений Azure — PowerShell | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate разгрузки шлюза приложения с помощью протокола SSL с помощью диспетчера ресурсов Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="cc601-103">Настройка шлюза приложений для разгрузки SSL с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="cc601-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc601-104">портал Azure</span><span class="sxs-lookup"><span data-stu-id="cc601-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="cc601-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="cc601-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="cc601-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc601-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="cc601-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cc601-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="cc601-108">Шлюз приложения Azure может быть настроенный tooterminate hello Secure Sockets Layer (SSL) сеанс при hello шлюза tooavoid дорогостоящих SSL расшифровки задачи toohappen на hello веб-фермы.</span><span class="sxs-lookup"><span data-stu-id="cc601-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="cc601-109">Разгрузка SSL также упрощает hello интерфейсном сервере настройку и управление ими hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cc601-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cc601-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="cc601-110">Before you begin</span></span>

1. <span data-ttu-id="cc601-111">Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello.</span><span class="sxs-lookup"><span data-stu-id="cc601-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="cc601-112">Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cc601-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="cc601-113">Создание виртуальной сети и подсети для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cc601-113">You create a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="cc601-114">Убедитесь, что нет виртуальных машин или развертывания в облаке hello подсети.</span><span class="sxs-lookup"><span data-stu-id="cc601-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="cc601-115">Сам шлюз приложений должен находиться в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="cc601-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="cc601-116">Настройка шлюза приложения hello toouse серверы Hello должен существовать или в виртуальной сети hello или открытый IP/VIP-адрес, назначенный создания конечных точек.</span><span class="sxs-lookup"><span data-stu-id="cc601-116">hello servers you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="cc601-117">Что такое необходимые toocreate шлюза приложения</span><span class="sxs-lookup"><span data-stu-id="cc601-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="cc601-118">**Пул серверных:** hello список IP-адресов серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="cc601-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="cc601-119">Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="cc601-119">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="cc601-120">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="cc601-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="cc601-121">Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="cc601-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="cc601-122">**Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cc601-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="cc601-123">Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="cc601-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="cc601-124">**Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти параметры зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).</span><span class="sxs-lookup"><span data-stu-id="cc601-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="cc601-125">**Правило:** правило hello привязывает прослушивателя hello и пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="cc601-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="cc601-126">В настоящее время только hello *основные* правило поддерживается.</span><span class="sxs-lookup"><span data-stu-id="cc601-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="cc601-127">Hello *основные* правило — распределение нагрузки с циклическим перебором.</span><span class="sxs-lookup"><span data-stu-id="cc601-127">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="cc601-128">**Дополнительные примечания по настройке конфигурации**</span><span class="sxs-lookup"><span data-stu-id="cc601-128">**Additional configuration notes**</span></span>

<span data-ttu-id="cc601-129">Для настройки сертификатов SSL, hello протокола в **HttpListener** следует изменить слишком*Https* (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="cc601-129">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="cc601-130">Hello **SslCertificate** слишком добавляется элемент**HttpListener** с hello значения переменной, настроенных для hello SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="cc601-130">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="cc601-131">Hello интерфейсный порт должен быть обновленные too443.</span><span class="sxs-lookup"><span data-stu-id="cc601-131">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="cc601-132">**сопоставление на основе файла cookie tooenable**: шлюза приложения может быть настроенный tooensure запроса из сеанса клиента всегда является направленным toohello одной виртуальной Машины hello веб-ферме.</span><span class="sxs-lookup"><span data-stu-id="cc601-132">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="cc601-133">Этот сценарий выполняется путем внедрения кода файла cookie сеанса, которое разрешает трафик toodirect шлюза hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="cc601-133">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="cc601-134">Задайте сопоставление на основе файла cookie tooenable **CookieBasedAffinity** слишком*включено* в hello **BackendHttpSettings** элемента.</span><span class="sxs-lookup"><span data-stu-id="cc601-134">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="cc601-135">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="cc601-135">Create an application gateway</span></span>

<span data-ttu-id="cc601-136">Создание шлюза и hello элементов приложения, требующие toobe настроен порядок hello указывается Hello различие между использованием hello Azure классической модели развертывания и диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="cc601-136">hello difference between using hello Azure Classic deployment model and Azure Resource Manager is hello order that you create an application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="cc601-137">С помощью диспетчера ресурсов все компоненты шлюза приложения настраиваются отдельно и затем поместить вместе toocreate шлюза ресурса приложения.</span><span class="sxs-lookup"><span data-stu-id="cc601-137">With Resource Manager, all components of an application gateway are configured individually and then put together toocreate an application gateway resource.</span></span>

<span data-ttu-id="cc601-138">Ниже приведены шаги, которые необходимы toocreate hello шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="cc601-138">Here are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="cc601-139">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="cc601-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="cc601-140">Создание виртуальной сети, подсети и общедоступный IP-адрес для шлюза приложения hello</span><span class="sxs-lookup"><span data-stu-id="cc601-140">Create virtual network, subnet, and public IP for hello application gateway</span></span>
3. <span data-ttu-id="cc601-141">Создание объекта конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="cc601-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="cc601-142">Создание ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="cc601-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="cc601-143">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="cc601-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="cc601-144">Убедитесь, что переключения командлеты PowerShell режим toouse hello диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="cc601-144">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="cc601-145">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cc601-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="cc601-146">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="cc601-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="cc601-147">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="cc601-147">Step 2</span></span>

<span data-ttu-id="cc601-148">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="cc601-148">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="cc601-149">С помощью учетных данных, запрашиваемых tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="cc601-149">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="cc601-150">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="cc601-150">Step 3</span></span>

<span data-ttu-id="cc601-151">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="cc601-151">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="cc601-152">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="cc601-152">Step 4</span></span>

<span data-ttu-id="cc601-153">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="cc601-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="cc601-154">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="cc601-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="cc601-155">Этот параметр используется в качестве расположения по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cc601-155">This setting is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="cc601-156">Убедитесь, что все команды toocreate, использует шлюз приложений hello таким же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cc601-156">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="cc601-157">В приведенном выше примере hello, мы создали группу ресурсов под названием **appgw RG** и расположение **Запад США**.</span><span class="sxs-lookup"><span data-stu-id="cc601-157">In hello example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="cc601-158">Создание виртуальной сети и подсети для шлюза приложения hello</span><span class="sxs-lookup"><span data-stu-id="cc601-158">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="cc601-159">Следующий пример показывает как Hello toocreate виртуальной сети с помощью диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="cc601-159">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="cc601-160">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="cc601-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="cc601-161">Этот образец присваивает hello диапазон адресов 10.0.0.0/24 tooa подсети переменной toobe используется toocreate виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="cc601-161">This sample assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="cc601-162">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="cc601-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="cc601-163">В этом примере создается виртуальная сеть с именем **appgwvnet** в группе ресурсов **appgw rg** для региона hello Запад США, с 10.0.0.0/16 hello префикс подсети 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="cc601-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="cc601-164">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="cc601-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="cc601-165">В этом примере назначает подсети hello объекта toovariable $subnet hello дальнейшими указаниями.</span><span class="sxs-lookup"><span data-stu-id="cc601-165">This sample assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="cc601-166">Создать общедоступный IP-адрес для интерфейса конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="cc601-166">Create a public IP address for hello front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="cc601-167">В этом примере создается открытому ресурсу IP **publicIP01** в группе ресурсов **appgw rg** для региона hello Запад США.</span><span class="sxs-lookup"><span data-stu-id="cc601-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="cc601-168">Создание объекта конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="cc601-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="cc601-169">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="cc601-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="cc601-170">Этот пример создает конфигурацию IP-адреса шлюза приложений с именем **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="cc601-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="cc601-171">При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и маршрутизацию сетевого трафика toohello IP-адресов в пул IP-адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="cc601-171">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="cc601-172">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="cc601-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="cc601-173">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="cc601-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="cc601-174">В этом примере настраивается hello серверной части IP-адресов с именем **pool01** с IP-адресами **134.170.185.46**, **134.170.188.221**, **134.170.185.50** .</span><span class="sxs-lookup"><span data-stu-id="cc601-174">This sample configures hello back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="cc601-175">Эти значения являются hello IP-адресов, получения сетевого трафика hello, поступающие от hello переднего плана конечную точку IP.</span><span class="sxs-lookup"><span data-stu-id="cc601-175">Those values are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="cc601-176">Замените hello IP-адресов из hello предшествующий пример hello IP-адреса вашего конечных точек веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cc601-176">Replace hello IP addresses from hello preceding example with hello IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="cc601-177">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="cc601-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="cc601-178">В этом примере настраиваются параметры шлюза приложения **poolsetting01** tooload трафика, обрабатываемого в пуле hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="cc601-178">This sample configures application gateway setting **poolsetting01** tooload-balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="cc601-179">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="cc601-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="cc601-180">В этом примере настраивается hello интерфейсный IP-порта с именем **frontendport01** для hello общедоступную конечную точку IP.</span><span class="sxs-lookup"><span data-stu-id="cc601-180">This sample configures hello front-end IP port named **frontendport01** for hello public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="cc601-181">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="cc601-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="cc601-182">В этом примере настраивается hello сертификат, используемый для подключения SSL.</span><span class="sxs-lookup"><span data-stu-id="cc601-182">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="cc601-183">Hello сертификат должен toobe в формате PFX и hello пароль должен содержать от 4 too12 символов.</span><span class="sxs-lookup"><span data-stu-id="cc601-183">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="cc601-184">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="cc601-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="cc601-185">В этом примере создается hello интерфейсный IP-конфигурации с именем **fipconfig01** и связывает hello общедоступный IP-адрес с hello интерфейсный IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cc601-185">This sample creates hello front-end IP configuration named **fipconfig01** and associates hello public IP address with hello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="cc601-186">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="cc601-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="cc601-187">В этом примере создается имя прослушивателя hello **listener01** и связывает hello интерфейсный порт toohello интерфейса конфигурации IP и сертификат.</span><span class="sxs-lookup"><span data-stu-id="cc601-187">This sample creates hello listener name **listener01** and associates hello front-end port toohello front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="cc601-188">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="cc601-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="cc601-189">В этом примере создается hello правило подсистемы балансировки нагрузки маршрутизации с именем **rule01** , предназначенный для настройки поведения подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="cc601-189">This sample creates hello load balancer routing rule named **rule01** that configures hello load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="cc601-190">Шаг 9.</span><span class="sxs-lookup"><span data-stu-id="cc601-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="cc601-191">В этом примере настраивается hello размер экземпляра шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cc601-191">This sample configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="cc601-192">Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10.</span><span class="sxs-lookup"><span data-stu-id="cc601-192">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="cc601-193">Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium.</span><span class="sxs-lookup"><span data-stu-id="cc601-193">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="cc601-194">Можно выбрать Standard_Small, Standard_Medium или Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="cc601-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="cc601-195">Шаг 10</span><span class="sxs-lookup"><span data-stu-id="cc601-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="cc601-196">Этот шаг определяет toouse политики hello SSL для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cc601-196">This step defines hello SSL policy toouse on hello application gateway.</span></span> <span data-ttu-id="cc601-197">Посетите [версии политики настройки SSL и комплектов шифров на использование шлюза приложений](application-gateway-configure-ssl-policy-powershell.md) toolearn дополнительные.</span><span class="sxs-lookup"><span data-stu-id="cc601-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="cc601-198">Создание шлюза приложений с помощью командлета New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="cc601-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="cc601-199">В этом примере создается шлюза приложения со всех элементов конфигурации из hello в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="cc601-199">This sample creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="cc601-200">В примере hello называется шлюза приложения hello **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="cc601-200">In hello example, hello application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="cc601-201">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="cc601-201">Get application gateway DNS name</span></span>

<span data-ttu-id="cc601-202">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="cc601-202">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="cc601-203">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="cc601-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="cc601-204">tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cc601-204">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="cc601-205">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cc601-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="cc601-206">toodo сведения, получение шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений.</span><span class="sxs-lookup"><span data-stu-id="cc601-206">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="cc601-207">шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="cc601-207">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="cc601-208">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="cc601-208">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="cc601-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc601-209">Next steps</span></span>

<span data-ttu-id="cc601-210">Если tooconfigure toouse шлюза приложения с внутренней подсистемы балансировки нагрузки (ILB), см. [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="cc601-210">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="cc601-211">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="cc601-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="cc601-212">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="cc601-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="cc601-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="cc601-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

