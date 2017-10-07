---
title: "aaaUsing шлюза приложения Azure с внутренним балансировщиком нагрузки - PowerShell | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, Настройка, запуск и удалить шлюз приложения Azure с внутренней подсистемы балансировки нагрузки (ILB) для диспетчера ресурсов Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="0fb1e-103">Создание шлюза приложений с внутренним балансировщиком нагрузки (ILB) с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="0fb1e-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0fb1e-104">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fb1e-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="0fb1e-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="0fb1e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="0fb1e-106">Шлюз приложения Azure можно настроить для виртуальных IP-адресов из Интернета или с внутренней конечной точки, не предоставляемых toohello Интернета, также называется конечной точкой (ILB) балансировщик внутренней нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed toohello Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="0fb1e-107">Настройка шлюза hello с ILB полезен для внутренних бизнес-приложений, не предоставляемых toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications that are not exposed toohello Internet.</span></span> <span data-ttu-id="0fb1e-108">Также полезно для служб и уровни в многоуровневое приложение, располагаются в пределах границ безопасности, не предоставляемых toohello Internet, но по-прежнему требуется циклическое загрузить распространения, stickiness сеанса или завершение Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="0fb1e-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed toohello Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="0fb1e-109">В этой статье рассматриваются действия hello tooconfigure шлюза приложения с ILB.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0fb1e-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="0fb1e-110">Before you begin</span></span>

1. <span data-ttu-id="0fb1e-111">Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="0fb1e-112">Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0fb1e-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="0fb1e-113">Вы создадите виртуальную сеть и подсеть для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="0fb1e-114">Убедитесь, что нет виртуальных машин или развертывания в облаке hello подсети.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="0fb1e-115">Сам шлюз приложений должен находиться в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="0fb1e-116">должен существовать настройки шлюза приложения hello toouse серверы Hello или назначенные их конечных точек, созданных в hello виртуальной сети или с помощью открытого IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="0fb1e-117">Что такое необходимые toocreate шлюза приложения</span><span class="sxs-lookup"><span data-stu-id="0fb1e-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="0fb1e-118">**Пул серверных:** hello список IP-адресов серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="0fb1e-119">Hello IP-адресов в списке должны либо относятся toohello виртуальной сети, но в другой подсети для шлюза приложения hello или должен быть открытый IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-119">hello IP addresses listed should either belong toohello virtual network but in a different subnet for hello application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="0fb1e-120">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="0fb1e-121">Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="0fb1e-122">**Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="0fb1e-123">Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="0fb1e-124">**Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, они зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).</span><span class="sxs-lookup"><span data-stu-id="0fb1e-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="0fb1e-125">**Правило:** правило hello привязывает прослушивателя hello и пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="0fb1e-126">В настоящее время только hello *основные* правило поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="0fb1e-127">Hello *основные* правило — распределение нагрузки с циклическим перебором.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-127">hello *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="0fb1e-128">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="0fb1e-128">Create an application gateway</span></span>

<span data-ttu-id="0fb1e-129">Hello различие между использованием классический Azure и Azure Resource Manager — создать шлюз приложения hello и hello элементы, которые должны toobe настроить порядок hello.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-129">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>
<span data-ttu-id="0fb1e-130">С помощью диспетчера ресурсов все элементы, которые делают шлюза приложения настроен по отдельности, а затем указать ресурс шлюза приложения hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-130">With Resource Manager, all items that make an application gateway is configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="0fb1e-131">Ниже приведены шаги hello, необходимые toocreate шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-131">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="0fb1e-132">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="0fb1e-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="0fb1e-133">Создание виртуальной сети и подсети для шлюза приложения hello</span><span class="sxs-lookup"><span data-stu-id="0fb1e-133">Create a virtual network and a subnet for hello application gateway</span></span>
3. <span data-ttu-id="0fb1e-134">Создание объекта конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="0fb1e-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="0fb1e-135">Создание ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="0fb1e-136">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="0fb1e-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="0fb1e-137">Убедитесь, что переключения командлеты PowerShell режим toouse hello диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-137">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="0fb1e-138">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0fb1e-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="0fb1e-139">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="0fb1e-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="0fb1e-140">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="0fb1e-140">Step 2</span></span>

<span data-ttu-id="0fb1e-141">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-141">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="0fb1e-142">С помощью учетных данных, запрашиваемых tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-142">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="0fb1e-143">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-143">Step 3</span></span>

<span data-ttu-id="0fb1e-144">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-144">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="0fb1e-145">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-145">Step 4</span></span>

<span data-ttu-id="0fb1e-146">Создайте группу ресурсов (если вы используете существующую группу, пропустите этот шаг).</span><span class="sxs-lookup"><span data-stu-id="0fb1e-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="0fb1e-147">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="0fb1e-148">Используется как расположение по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-148">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="0fb1e-149">Убедитесь, что все команды toocreate, использует шлюз приложений hello таким же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-149">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="0fb1e-150">В предыдущих пример hello мы создали группу ресурсов под названием «Appgw rg» и расположение «West US».</span><span class="sxs-lookup"><span data-stu-id="0fb1e-150">In hello preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="0fb1e-151">Создание виртуальной сети и подсети для шлюза приложения hello</span><span class="sxs-lookup"><span data-stu-id="0fb1e-151">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="0fb1e-152">Следующий пример показывает как Hello toocreate виртуальной сети с помощью диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="0fb1e-152">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="0fb1e-153">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="0fb1e-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="0fb1e-154">Этот шаг назначает hello диапазон адресов 10.0.0.0/24 tooa подсети переменной toobe используется toocreate виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-154">This step assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="0fb1e-155">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="0fb1e-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="0fb1e-156">Этот шаг создает виртуальную сеть с именем «appgwvnet» в ресурс группы «appgw-rg» для области hello Запад США, с 10.0.0.0/16 hello префикс подсети 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="0fb1e-157">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="0fb1e-158">Этот шаг назначает подсети hello объекта toovariable $subnet hello дальнейшими указаниями.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-158">This step assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="0fb1e-159">Создание объекта конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="0fb1e-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="0fb1e-160">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="0fb1e-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="0fb1e-161">На этом шаге создается конфигурация IP-адреса шлюза приложений с именем gatewayIP01.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="0fb1e-162">При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и маршрутизацию сетевого трафика toohello IP-адресов в пул IP-адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-162">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="0fb1e-163">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="0fb1e-164">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="0fb1e-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="0fb1e-165">Этот шаг позволяет настроить hello серверной части IP-адресов с именем «pool01» с IP-адреса «10.1.1.8, 10.1.1.9, 10.1.1.10».</span><span class="sxs-lookup"><span data-stu-id="0fb1e-165">This step configures hello back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="0fb1e-166">Это и есть hello IP-адресов, получения сетевого трафика hello, поступающие от hello переднего плана конечную точку IP.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-166">Those are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="0fb1e-167">Замените hello предшествующий IP адресов tooadd собственных конечных точек приложения IP адрес.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-167">You replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="0fb1e-168">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="0fb1e-169">Этот шаг позволяет настроить приложения шлюза параметр «poolsetting01» для загрузки hello балансировки сетевой трафик в пуле hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-169">This step configures application gateway setting "poolsetting01" for hello load balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="0fb1e-170">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="0fb1e-171">Этот шаг позволяет настроить hello интерфейсный IP-порта с именем «frontendport01» для hello ILB.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-171">This step configures hello front-end IP port named "frontendport01" for hello ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="0fb1e-172">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="0fb1e-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="0fb1e-173">Этот шаг создает hello интерфейсный IP-конфигурация называется «fipconfig01» и связывает его с частный IP-адрес в подсети виртуальной сети текущего hello.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-173">This step creates hello front-end IP configuration called "fipconfig01" and associates it with a private IP from hello current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="0fb1e-174">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="0fb1e-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="0fb1e-175">Этот шаг создает hello прослушивателя с именем «listener01» и связывает hello интерфейсный порт toohello интерфейсный IP конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-175">This step creates hello listener called "listener01" and associates hello front-end port toohello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="0fb1e-176">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="0fb1e-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="0fb1e-177">На этом шаге создается hello правило подсистемы балансировки нагрузки маршрутизации называется «rule01», предназначенный для настройки поведения подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-177">This step creates hello load balancer routing rule called "rule01" that configures hello load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="0fb1e-178">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="0fb1e-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="0fb1e-179">Этот шаг позволяет настроить размер экземпляра hello шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-179">This step configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="0fb1e-180">Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-180">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="0fb1e-181">Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-181">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="0fb1e-182">Можно выбрать Standard_Small, Standard_Medium или Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="0fb1e-183">Создание шлюза приложений с помощью командлета New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="0fb1e-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="0fb1e-184">Создает все элементы конфигурации из предыдущих шагах hello шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-184">Creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="0fb1e-185">В этом примере шлюза приложения hello называется «appgwtest».</span><span class="sxs-lookup"><span data-stu-id="0fb1e-185">In this example, hello application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="0fb1e-186">На этом шаге создается шлюза приложения со всех элементов конфигурации из hello в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-186">This step creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="0fb1e-187">В примере hello шлюза приложения hello называется «appgwtest».</span><span class="sxs-lookup"><span data-stu-id="0fb1e-187">In hello example, hello application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="0fb1e-188">Удаление шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="0fb1e-188">Delete an application gateway</span></span>

<span data-ttu-id="0fb1e-189">toodelete шлюза приложения необходимые hello toodo следующие шаги в порядке.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-189">toodelete an application gateway, you need toodo hello following steps in order:</span></span>

1. <span data-ttu-id="0fb1e-190">Используйте hello `Stop-AzureRmApplicationGateway` командлет toostop hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-190">Use hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="0fb1e-191">Используйте hello `Remove-AzureRmApplicationGateway` командлет tooremove hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-191">Use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="0fb1e-192">Убедитесь, что hello шлюза был удален с помощью hello `Get-AzureApplicationGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-192">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="0fb1e-193">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="0fb1e-193">Step 1</span></span>

<span data-ttu-id="0fb1e-194">Получите объект шлюза приложения hello и связать его переменной tooa «$getgw».</span><span class="sxs-lookup"><span data-stu-id="0fb1e-194">Get hello application gateway object and associate it tooa variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="0fb1e-195">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="0fb1e-195">Step 2</span></span>

<span data-ttu-id="0fb1e-196">Используйте `Stop-AzureRmApplicationGateway` toostop шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-196">Use `Stop-AzureRmApplicationGateway` toostop hello application gateway.</span></span> <span data-ttu-id="0fb1e-197">В этом примере показано hello `Stop-AzureRmApplicationGateway` на первую строку hello, командлет следуют hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-197">This sample shows hello `Stop-AzureRmApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="0fb1e-198">После шлюза приложения hello в остановленном состоянии используйте hello `Remove-AzureRmApplicationGateway` командлет tooremove hello службы.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-198">Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> <span data-ttu-id="0fb1e-199">Hello **-принудительно** коммутатор может быть сообщение с подтверждением remove используется toosuppress hello.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-199">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="0fb1e-200">tooverify, hello службы были удалены, вы можете использовать hello `Get-AzureRmApplicationGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-200">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="0fb1e-201">Этот шаг не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="0fb1e-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="0fb1e-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0fb1e-202">Next steps</span></span>

<span data-ttu-id="0fb1e-203">Если tooconfigure разгрузки SSL, см. [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="0fb1e-203">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="0fb1e-204">Tooconfigure toouse шлюза приложения с ILB см [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="0fb1e-204">If you want tooconfigure an application gateway toouse with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="0fb1e-205">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="0fb1e-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="0fb1e-206">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="0fb1e-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="0fb1e-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0fb1e-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

