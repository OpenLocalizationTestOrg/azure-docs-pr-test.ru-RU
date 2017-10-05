---
title: "Настройка разгрузки SSL для шлюза приложений Azure с помощью PowerShell | Документация Майкрософт"
description: "На этой странице приводятся инструкции по созданию шлюза приложений с разгрузкой SSL с помощью диспетчера ресурсов Azure."
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
ms.openlocfilehash: ededabc7c665d6bb05b91e4d21d01fb1379add32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="dd540-103">Настройка шлюза приложений для разгрузки SSL с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="dd540-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd540-104">портал Azure</span><span class="sxs-lookup"><span data-stu-id="dd540-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="dd540-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="dd540-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="dd540-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd540-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="dd540-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dd540-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="dd540-108">Шлюз приложений Azure можно настроить на завершение сеанса SSL в шлюзе, что позволит избежать выполнения дорогостоящей задачи SSL-шифрования на веб-ферме.</span><span class="sxs-lookup"><span data-stu-id="dd540-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="dd540-109">Кроме того, разгрузка SSL упрощает процесс установки внешнего сервера и управления веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="dd540-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dd540-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="dd540-110">Before you begin</span></span>

1. <span data-ttu-id="dd540-111">Установите последнюю версию командлетов Azure PowerShell, используя установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="dd540-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="dd540-112">Скачать и установить последнюю версию вы можете в разделе **Windows PowerShell** на [странице загрузок](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="dd540-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="dd540-113">Создайте виртуальную сеть и подсеть для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="dd540-113">You create a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="dd540-114">Убедитесь, что подсеть не используется виртуальной машиной или облачным развертыванием.</span><span class="sxs-lookup"><span data-stu-id="dd540-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="dd540-115">Сам шлюз приложений должен находиться в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="dd540-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="dd540-116">Для использования шлюза приложений настраиваются существующие серверы или серверы, для которых в виртуальной сети созданы конечные точки либо же назначен общедоступный или виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="dd540-116">The servers you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="dd540-117">Что необходимо для создания шлюза приложений?</span><span class="sxs-lookup"><span data-stu-id="dd540-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="dd540-118">**Внутренний пул серверов**. Список IP-адресов внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="dd540-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="dd540-119">Указанные IP-адреса должны относиться к подсети виртуальной сети либо представлять собой общедоступные или виртуальные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="dd540-119">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="dd540-120">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="dd540-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="dd540-121">Эти параметры привязываются к пулу и применяются ко всем серверам в этом пуле.</span><span class="sxs-lookup"><span data-stu-id="dd540-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="dd540-122">**Интерфейсный порт**. Общедоступный порт, открытый в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="dd540-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="dd540-123">Трафик поступает на этот порт, а затем перенаправляется на один из тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="dd540-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="dd540-124">**Прослушиватель**. У прослушивателя есть интерфейсный порт, протокол (Http или Https, с учетом регистра) и имя SSL-сертификата (при настройке разгрузки SSL).</span><span class="sxs-lookup"><span data-stu-id="dd540-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="dd540-125">**Правило**. Правило связывает прослушиватель и внутренний пул серверов, а также определяет, в какой внутренний пул серверов следует направлять трафик, поступающий на определенный прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="dd540-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="dd540-126">В настоящее время поддерживается только *основное* правило.</span><span class="sxs-lookup"><span data-stu-id="dd540-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="dd540-127">*Основное* правило предусматривает циклическое распределение нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd540-127">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="dd540-128">**Дополнительные примечания по настройке конфигурации**</span><span class="sxs-lookup"><span data-stu-id="dd540-128">**Additional configuration notes**</span></span>

<span data-ttu-id="dd540-129">Чтобы настроить конфигурацию SSL-сертификатов, протокол в элементе **HttpListener** следует изменить на *Https* (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="dd540-129">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="dd540-130">Элемент **SslCertificate** нужно добавить в **HttpListener**, указав в качестве значения переменную, настроенную для SSL-сертификата.</span><span class="sxs-lookup"><span data-stu-id="dd540-130">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="dd540-131">Внешний порт следует изменить на 443.</span><span class="sxs-lookup"><span data-stu-id="dd540-131">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="dd540-132">**Включение сходства на основе файлов cookie**. Шлюз приложений можно настроить так, чтобы запросы от клиентского сеанса всегда направлялись на одну виртуальную машину в веб-ферме.</span><span class="sxs-lookup"><span data-stu-id="dd540-132">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="dd540-133">Это делается с помощью внедрения файлов cookie сеанса, что позволяет шлюзу перенаправлять трафик соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="dd540-133">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="dd540-134">Чтобы включить сходство на основе файлов cookie, присвойте параметру **CookieBasedAffinity** в элементе *BackendHttpSettings* значение **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="dd540-134">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="dd540-135">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="dd540-135">Create an application gateway</span></span>

<span data-ttu-id="dd540-136">Разница между использованием классической модели развертывания Azure и Azure Resource Manager заключается в порядке создания шлюза приложений и элементов, которые нужно настроить.</span><span class="sxs-lookup"><span data-stu-id="dd540-136">The difference between using the Azure Classic deployment model and Azure Resource Manager is the order that you create an application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="dd540-137">При использовании Resource Manager все компоненты, которые будут включены в единый ресурс шлюза приложений, сначала настраиваются по отдельности.</span><span class="sxs-lookup"><span data-stu-id="dd540-137">With Resource Manager, all components of an application gateway are configured individually and then put together to create an application gateway resource.</span></span>

<span data-ttu-id="dd540-138">Ниже приведены пошаговые инструкции по созданию шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="dd540-138">Here are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="dd540-139">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="dd540-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="dd540-140">Создание виртуальной сети, подсети и общедоступного IP-адреса для шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="dd540-140">Create virtual network, subnet, and public IP for the application gateway</span></span>
3. <span data-ttu-id="dd540-141">Создание объекта конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="dd540-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="dd540-142">Создание ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="dd540-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="dd540-143">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="dd540-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="dd540-144">Для работы с командлетами диспетчера ресурсов Azure необходимо перейти в режим PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd540-144">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="dd540-145">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="dd540-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="dd540-146">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="dd540-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="dd540-147">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="dd540-147">Step 2</span></span>

<span data-ttu-id="dd540-148">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="dd540-148">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="dd540-149">Вам будет предложено указать свои учетные данные для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="dd540-149">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="dd540-150">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="dd540-150">Step 3</span></span>

<span data-ttu-id="dd540-151">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="dd540-151">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="dd540-152">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="dd540-152">Step 4</span></span>

<span data-ttu-id="dd540-153">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="dd540-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="dd540-154">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="dd540-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="dd540-155">Оно используется в качестве расположения по умолчанию для всех ресурсов данной группы.</span><span class="sxs-lookup"><span data-stu-id="dd540-155">This setting is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="dd540-156">Убедитесь, что во всех командах для создания шлюза приложений используется одна группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="dd540-156">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="dd540-157">В приведенном выше примере мы создали группу ресурсов с именем **appgw-RG** и расположением **Западная часть США**.</span><span class="sxs-lookup"><span data-stu-id="dd540-157">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="dd540-158">Создание виртуальной сети и подсети для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="dd540-158">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="dd540-159">В следующем примере показано создание виртуальной сети с помощью диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="dd540-159">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="dd540-160">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="dd540-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="dd540-161">Этот пример назначает диапазон адресов 10.0.0.0/24 переменной подсети, которая будет использоваться для создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="dd540-161">This sample assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="dd540-162">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="dd540-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="dd540-163">Этот пример создает виртуальную сеть **appgwvnet** в группе ресурсов **appgw-rg** для региона "Западная часть США" с помощью префикса 10.0.0.0/16 с подсетью 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="dd540-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="dd540-164">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="dd540-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="dd540-165">Этот пример присваивает объект подсети переменной $subnet для выполнения следующих действий.</span><span class="sxs-lookup"><span data-stu-id="dd540-165">This sample assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="dd540-166">Создание общедоступного IP-адреса для конфигурации интерфейсной части</span><span class="sxs-lookup"><span data-stu-id="dd540-166">Create a public IP address for the front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="dd540-167">Этот пример создает ресурс общедоступного IP-адреса **publicIP01** в группе ресурсов **appgw-rg** для региона "Западная часть США".</span><span class="sxs-lookup"><span data-stu-id="dd540-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="dd540-168">Создание объекта конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="dd540-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="dd540-169">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="dd540-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="dd540-170">Этот пример создает конфигурацию IP-адреса шлюза приложений с именем **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="dd540-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="dd540-171">При запуске шлюз приложений получает IP-адрес из настроенной подсети. Затем шлюз маршрутизирует сетевой трафик на IP-адреса из внутреннего пула IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="dd540-171">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="dd540-172">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="dd540-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="dd540-173">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="dd540-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="dd540-174">Этот пример настраивает пул внутренних IP-адресов с именем **pool01** и IP-адресами **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span><span class="sxs-lookup"><span data-stu-id="dd540-174">This sample configures the back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="dd540-175">Эти значения IP-адресов будут использоваться для получения сетевого трафика от конечной точки с интерфейсным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="dd540-175">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="dd540-176">Замените IP-адрес в предыдущем примере IP-адресом конечных точек вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="dd540-176">Replace the IP addresses from the preceding example with the IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="dd540-177">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="dd540-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="dd540-178">Этот пример настраивает параметр шлюза приложений **poolsetting01** для балансировки нагрузки сетевого трафика в пуле серверной части.</span><span class="sxs-lookup"><span data-stu-id="dd540-178">This sample configures application gateway setting **poolsetting01** to load-balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="dd540-179">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="dd540-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="dd540-180">Этот пример настраивает внешний IP-порт **frontendport01** для конечной точки с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="dd540-180">This sample configures the front-end IP port named **frontendport01** for the public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="dd540-181">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="dd540-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="dd540-182">Этот пример настраивает сертификат для SSL-соединения.</span><span class="sxs-lookup"><span data-stu-id="dd540-182">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="dd540-183">Сертификат должен быть в формате PFX, а пароль к сертификату должен содержать от 4 до 12 символов.</span><span class="sxs-lookup"><span data-stu-id="dd540-183">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="dd540-184">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="dd540-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="dd540-185">Этот пример создает конфигурацию внешнего IP-адреса с именем **fipconfig01** и связывает с ней общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="dd540-185">This sample creates the front-end IP configuration named **fipconfig01** and associates the public IP address with the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="dd540-186">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="dd540-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="dd540-187">Этот пример создает прослушиватель **listener01** и связывает внешний порт с конфигурацией внешнего IP-адреса и сертификатом.</span><span class="sxs-lookup"><span data-stu-id="dd540-187">This sample creates the listener name **listener01** and associates the front-end port to the front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="dd540-188">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="dd540-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="dd540-189">Этот пример создает правило маршрутизации **rule01** для настройки поведения подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dd540-189">This sample creates the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="dd540-190">Шаг 9.</span><span class="sxs-lookup"><span data-stu-id="dd540-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="dd540-191">Этот пример настраивает размер экземпляра шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="dd540-191">This sample configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="dd540-192">Значение параметра *InstanceCount* по умолчанию — 2 (максимальное значение — 10).</span><span class="sxs-lookup"><span data-stu-id="dd540-192">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="dd540-193">Значение *GatewaySize* (Размер шлюза) по умолчанию — Medium (Средний).</span><span class="sxs-lookup"><span data-stu-id="dd540-193">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="dd540-194">Можно выбрать Standard_Small, Standard_Medium или Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="dd540-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="dd540-195">Шаг 10</span><span class="sxs-lookup"><span data-stu-id="dd540-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="dd540-196">На этом шаге выполняется настройка политики SSL для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="dd540-196">This step defines the SSL policy to use on the application gateway.</span></span> <span data-ttu-id="dd540-197">Дополнительные сведения см. в статье [Настройка версий политики SSL и комплектов шифров на шлюзе приложений](application-gateway-configure-ssl-policy-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dd540-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="dd540-198">Создание шлюза приложений с помощью командлета New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="dd540-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="dd540-199">Этот пример создает шлюз приложений со всеми элементами конфигурации, описанными выше.</span><span class="sxs-lookup"><span data-stu-id="dd540-199">This sample creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="dd540-200">В этом примере шлюз приложений называется **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="dd540-200">In the example, the application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="dd540-201">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="dd540-201">Get application gateway DNS name</span></span>

<span data-ttu-id="dd540-202">После создания шлюза следует настроить внешний интерфейс для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="dd540-202">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="dd540-203">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="dd540-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="dd540-204">Чтобы гарантировать попадание пользователей на шлюз приложений, можно использовать запись CNAME, чтобы указать общедоступную конечную точку шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="dd540-204">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="dd540-205">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dd540-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="dd540-206">Получите информацию о шлюзе приложений и соответствующее IP- или DNS-имя с помощью элемента PublicIPAddress, связанного со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="dd540-206">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="dd540-207">DNS-имя шлюза приложений должно использоваться для создания записи CNAME, указывающей двум веб-приложениям на это DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="dd540-207">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="dd540-208">Использование записи A не рекомендуется, так как виртуальный IP-адрес может измениться после перезапуска приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="dd540-208">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="dd540-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd540-209">Next steps</span></span>

<span data-ttu-id="dd540-210">Указания по настройке шлюза приложений для использования с внутренним балансировщиком нагрузки см. в статье [Создание шлюза приложений с внутренним балансировщиком нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="dd540-210">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="dd540-211">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="dd540-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="dd540-212">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="dd540-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="dd540-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="dd540-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

