---
title: "Использование шлюза приложения Azure с внутренней подсистемой балансировки нагрузки с помощью PowerShell | Документация Майкрософт"
description: "На этой странице приводятся инструкции по созданию, настройке, запуску и удалению шлюза приложений Azure с внутренним балансировщиком нагрузки (ILB) с помощью диспетчера ресурсов Azure."
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
ms.openlocfilehash: d218eab7e9f124e4825a8a781b4eeb0dcca58b4a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="a9994-103">Создание шлюза приложений с внутренним балансировщиком нагрузки (ILB) с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="a9994-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9994-104">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9994-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="a9994-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="a9994-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="a9994-106">Шлюз приложений Azure можно настроить на использование виртуального IP-адреса, доступного в Интернете, или внутренней конечной точки, недоступной в Интернете. Эта точка также называется конечной точкой внутреннего балансировщика нагрузки (ILB).</span><span class="sxs-lookup"><span data-stu-id="a9994-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed to the Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="a9994-107">Настройка шлюза с ILB подходит для внутренних бизнес-приложений, недоступных в Интернете.</span><span class="sxs-lookup"><span data-stu-id="a9994-107">Configuring the gateway with an ILB is useful for internal line-of-business applications that are not exposed to the Internet.</span></span> <span data-ttu-id="a9994-108">Кроме того, этот вариант конфигурации можно использовать для служб и уровней многоуровневого приложения, размещенного в периметре безопасности без доступа к Интернету, но требующего циклического перебора нагрузки, закрепления сеансов или завершения SSL-запросов.</span><span class="sxs-lookup"><span data-stu-id="a9994-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed to the Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="a9994-109">В этой статье приводятся пошаговые инструкции по настройке шлюза приложений с использованием ILB.</span><span class="sxs-lookup"><span data-stu-id="a9994-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a9994-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a9994-110">Before you begin</span></span>

1. <span data-ttu-id="a9994-111">Установите последнюю версию командлетов Azure PowerShell, используя установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="a9994-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="a9994-112">Последнюю версию можно загрузить и установить в разделе **Windows PowerShell** на [странице загрузок](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a9994-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="a9994-113">Вы создадите виртуальную сеть и подсеть для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a9994-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="a9994-114">Убедитесь, что подсеть не используется виртуальной машиной или облачным развертыванием.</span><span class="sxs-lookup"><span data-stu-id="a9994-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="a9994-115">Сам шлюз приложений должен находиться в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a9994-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="a9994-116">Для использования шлюза приложений настраиваются существующие серверы или серверы, для которых в виртуальной сети созданы конечные точки либо же назначен общедоступный или виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a9994-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="a9994-117">Что необходимо для создания шлюза приложений?</span><span class="sxs-lookup"><span data-stu-id="a9994-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="a9994-118">**Внутренний пул серверов**. Список IP-адресов внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="a9994-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="a9994-119">Указанные IP-адреса должны относиться к одной виртуальной сети (но не входить в подсеть шлюза приложений) либо представлять собой общедоступные или виртуальные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="a9994-119">The IP addresses listed should either belong to the virtual network but in a different subnet for the application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="a9994-120">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="a9994-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="a9994-121">Эти параметры привязываются к пулу и применяются ко всем серверам в этом пуле.</span><span class="sxs-lookup"><span data-stu-id="a9994-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="a9994-122">**Интерфейсный порт**. Общедоступный порт, открытый в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="a9994-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="a9994-123">Трафик поступает на этот порт, а затем перенаправляется на один из тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="a9994-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="a9994-124">**Прослушиватель**. У прослушивателя есть интерфейсный порт, протокол (Http или Https — с учетом регистра) и имя SSL-сертификата (в случае настройки разгрузки SSL).</span><span class="sxs-lookup"><span data-stu-id="a9994-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="a9994-125">**Правило**. Правило связывает прослушиватель и внутренний пул серверов, а также определяет, в какой внутренний пул серверов следует направлять трафик, поступающий на определенный прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="a9994-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="a9994-126">В настоящее время поддерживается только *основное* правило.</span><span class="sxs-lookup"><span data-stu-id="a9994-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="a9994-127">*Основное* правило предусматривает циклическое распределение нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a9994-127">The *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="a9994-128">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a9994-128">Create an application gateway</span></span>

<span data-ttu-id="a9994-129">Разница между использованием классической модели развертывания Azure и модели Azure Resource Manager заключается в порядке создания шлюза приложения и элементов, которые нужно настроить.</span><span class="sxs-lookup"><span data-stu-id="a9994-129">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>
<span data-ttu-id="a9994-130">При использовании Resource Manager все элементы, которые будут включены в единый ресурс шлюза приложений, сначала настраиваются по отдельности.</span><span class="sxs-lookup"><span data-stu-id="a9994-130">With Resource Manager, all items that make an application gateway is configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="a9994-131">Ниже приведены пошаговые инструкции по созданию шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a9994-131">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="a9994-132">Создание группы ресурсов для диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a9994-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="a9994-133">Создание виртуальной сети и подсети для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a9994-133">Create a virtual network and a subnet for the application gateway</span></span>
3. <span data-ttu-id="a9994-134">Создание объекта конфигурации шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a9994-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="a9994-135">Создание ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a9994-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="a9994-136">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="a9994-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="a9994-137">Для работы с командлетами диспетчера ресурсов Azure необходимо перейти в режим PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9994-137">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="a9994-138">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a9994-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="a9994-139">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a9994-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="a9994-140">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a9994-140">Step 2</span></span>

<span data-ttu-id="a9994-141">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a9994-141">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="a9994-142">Вам будет предложено указать свои учетные данные для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="a9994-142">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="a9994-143">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="a9994-143">Step 3</span></span>

<span data-ttu-id="a9994-144">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="a9994-144">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="a9994-145">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="a9994-145">Step 4</span></span>

<span data-ttu-id="a9994-146">Создайте группу ресурсов (если вы используете существующую группу, пропустите этот шаг).</span><span class="sxs-lookup"><span data-stu-id="a9994-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="a9994-147">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="a9994-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="a9994-148">Оно используется в качестве расположения по умолчанию для всех ресурсов данной группы.</span><span class="sxs-lookup"><span data-stu-id="a9994-148">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="a9994-149">Убедитесь, что во всех командах для создания шлюза приложений используется одна группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a9994-149">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="a9994-150">В приведенном выше примере мы создали группу ресурсов appgw-rg в расположении West US (западная часть США).</span><span class="sxs-lookup"><span data-stu-id="a9994-150">In the preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="a9994-151">Создание виртуальной сети и подсети для шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a9994-151">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="a9994-152">В следующем примере показано создание виртуальной сети с помощью диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a9994-152">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="a9994-153">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a9994-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="a9994-154">На этом шаге выполняется назначение диапазона адресов 10.0.0.0/24 переменной подсети, которая будет использоваться для создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a9994-154">This step assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="a9994-155">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a9994-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="a9994-156">На этом шаге создается виртуальная сеть appgwvnet в группе ресурсов appgw-rg для региона West US с помощью префикса 10.0.0.0/16 с подсетью 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="a9994-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="a9994-157">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="a9994-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="a9994-158">На этом шаге выполняется присвоение объекта подсети переменной $subnet для выполнения следующих действий.</span><span class="sxs-lookup"><span data-stu-id="a9994-158">This step assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="a9994-159">Создание объекта конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a9994-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="a9994-160">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a9994-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="a9994-161">На этом шаге создается конфигурация IP-адреса шлюза приложений с именем gatewayIP01.</span><span class="sxs-lookup"><span data-stu-id="a9994-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="a9994-162">При запуске шлюз приложений получает IP-адрес из настроенной подсети. Затем шлюз маршрутизирует сетевой трафик на IP-адреса из внутреннего пула IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a9994-162">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="a9994-163">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a9994-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="a9994-164">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a9994-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="a9994-165">В этом шаге выполняется настройка внутреннего пула IP-адресов pool01 с IP-адресами 10.1.1.8, 10.1.1.9, 10.1.1.10.</span><span class="sxs-lookup"><span data-stu-id="a9994-165">This step configures the back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="a9994-166">Эти адреса будут использоваться для получения сетевого трафика от конечной точки с интерфейсным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="a9994-166">Those are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="a9994-167">Замените приведенные выше IP-адреса и добавьте IP-адреса конечных точек своего приложения.</span><span class="sxs-lookup"><span data-stu-id="a9994-167">You replace the preceding IP addresses to add your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="a9994-168">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="a9994-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="a9994-169">На этом шаге осуществляется настройка параметров шлюза приложений poolsetting01 для балансировки нагрузки сетевого трафика в пуле серверной части.</span><span class="sxs-lookup"><span data-stu-id="a9994-169">This step configures application gateway setting "poolsetting01" for the load balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="a9994-170">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="a9994-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="a9994-171">На этом шаге выполняется настройка внешнего IP-порта с именем frontendport01 для внутренней подсистемы балансировки нагрузки (ILB).</span><span class="sxs-lookup"><span data-stu-id="a9994-171">This step configures the front-end IP port named "frontendport01" for the ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="a9994-172">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="a9994-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="a9994-173">На этом шаге выполняется создание конфигурации внешнего IP-адреса с именем fipconfig01 и ее связывание с частным IP-адресом из текущей подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a9994-173">This step creates the front-end IP configuration called "fipconfig01" and associates it with a private IP from the current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="a9994-174">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="a9994-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="a9994-175">На этом шаге выполняется создание прослушивателя listener01 и связывание внешнего порта с конфигурацией внешнего IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="a9994-175">This step creates the listener called "listener01" and associates the front-end port to the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="a9994-176">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="a9994-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="a9994-177">На этом шаге выполняется создание правила маршрутизации rule01 для настройки поведения подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a9994-177">This step creates the load balancer routing rule called "rule01" that configures the load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="a9994-178">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="a9994-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="a9994-179">На этом шаге выполняется настройка размера экземпляра шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a9994-179">This step configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="a9994-180">Значение параметра *InstanceCount* по умолчанию — 2 (максимальное значение — 10).</span><span class="sxs-lookup"><span data-stu-id="a9994-180">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="a9994-181">Значение *GatewaySize* (Размер шлюза) по умолчанию — Medium (Средний).</span><span class="sxs-lookup"><span data-stu-id="a9994-181">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="a9994-182">Можно выбрать Standard_Small, Standard_Medium или Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="a9994-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="a9994-183">Создание шлюза приложений с помощью командлета New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="a9994-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="a9994-184">Создайте шлюз приложений со всеми элементами конфигурации, описанными выше.</span><span class="sxs-lookup"><span data-stu-id="a9994-184">Creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="a9994-185">В этом примере шлюз приложений называется "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="a9994-185">In this example, the application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="a9994-186">На этом шаге создается шлюз приложений со всеми элементами конфигурации, описанными выше.</span><span class="sxs-lookup"><span data-stu-id="a9994-186">This step creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="a9994-187">В этом примере шлюз приложений называется appgwtest.</span><span class="sxs-lookup"><span data-stu-id="a9994-187">In the example, the application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="a9994-188">Удаление шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a9994-188">Delete an application gateway</span></span>

<span data-ttu-id="a9994-189">Чтобы удалить шлюз приложений, по порядку выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="a9994-189">To delete an application gateway, you need to do the following steps in order:</span></span>

1. <span data-ttu-id="a9994-190">Остановите шлюз с помощью командлета `Stop-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="a9994-190">Use the `Stop-AzureRmApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="a9994-191">Удалите шлюз с помощью командлета `Remove-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="a9994-191">Use the `Remove-AzureRmApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="a9994-192">С помощью командлета `Get-AzureApplicationGateway` проверьте, удален ли шлюз.</span><span class="sxs-lookup"><span data-stu-id="a9994-192">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="a9994-193">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a9994-193">Step 1</span></span>

<span data-ttu-id="a9994-194">Получите объект шлюза приложений и свяжите его с переменной $getgw.</span><span class="sxs-lookup"><span data-stu-id="a9994-194">Get the application gateway object and associate it to a variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="a9994-195">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a9994-195">Step 2</span></span>

<span data-ttu-id="a9994-196">С помощью командлета `Stop-AzureRmApplicationGateway` остановите шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="a9994-196">Use `Stop-AzureRmApplicationGateway` to stop the application gateway.</span></span> <span data-ttu-id="a9994-197">В данном примере командлет `Stop-AzureRmApplicationGateway` показан в первой строке, а за ним следуют выходные данные.</span><span class="sxs-lookup"><span data-stu-id="a9994-197">This sample shows the `Stop-AzureRmApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

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

<span data-ttu-id="a9994-198">Когда шлюз будет остановлен, удалите службу с помощью командлета `Remove-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="a9994-198">Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.</span></span>

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
> <span data-ttu-id="a9994-199">Если указать параметр **-force** , запрос на подтверждение удаления не появится.</span><span class="sxs-lookup"><span data-stu-id="a9994-199">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="a9994-200">Для проверки того, удалена ли служба, используйте командлет `Get-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="a9994-200">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="a9994-201">Этот шаг не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="a9994-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="a9994-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a9994-202">Next steps</span></span>

<span data-ttu-id="a9994-203">Чтобы настроить разгрузку SSL, ознакомьтесь с [настройкой шлюза приложений для разгрузки SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="a9994-203">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="a9994-204">Указания по настройке шлюза приложений для использования с внутренним балансировщиком нагрузки см. в статье [Создание шлюза приложений с внутренней подсистемой балансировки нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="a9994-204">If you want to configure an application gateway to use with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="a9994-205">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="a9994-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="a9994-206">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="a9994-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="a9994-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="a9994-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

