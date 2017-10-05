---
title: "Создание шлюза приложений с помощью правил маршрутизации URL-адресов | Документация Майкрософт"
description: "На этой странице приводятся инструкции по созданию и настройке шлюза приложений Azure с помощью правил маршрутизации URL-адресов."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: ba756d3262b9780c5701e69faad860ba32bba08b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="2791a-103">Создание шлюза приложений с помощью маршрутизации на основе пути</span><span class="sxs-lookup"><span data-stu-id="2791a-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2791a-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="2791a-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="2791a-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="2791a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="2791a-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2791a-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="2791a-107">Маршрутизация на основе URL-адресов позволяет связывать маршруты на основе URL-пути HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="2791a-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="2791a-108">Она позволяет проверить, настроен ли для URL-адреса в шлюзе приложений маршрут к внутреннему пулу.</span><span class="sxs-lookup"><span data-stu-id="2791a-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway.</span></span> <span data-ttu-id="2791a-109">После этого сетевой трафик передается в определенный внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="2791a-109">It then sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="2791a-110">Как правило, маршрутизация на основе URL-адресов используется для распределения запросов содержимого разных типов между разными пулами тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="2791a-110">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="2791a-111">При маршрутизации на основе URL-адресов к шлюзу приложений добавляется новый тип правил.</span><span class="sxs-lookup"><span data-stu-id="2791a-111">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="2791a-112">Шлюз приложений имеет два типа правил: базовые правила и правила на основе пути.</span><span class="sxs-lookup"><span data-stu-id="2791a-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="2791a-113">Основной тип правил обеспечивает циклическое обслуживание пулов тыловых серверов, а PathBasedRouting наряду с циклическим распространением при выборе пула тыловых серверов учитывает также шаблон URL-адреса запроса.</span><span class="sxs-lookup"><span data-stu-id="2791a-113">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="2791a-114">Сценарий</span><span class="sxs-lookup"><span data-stu-id="2791a-114">Scenario</span></span>

<span data-ttu-id="2791a-115">В следующем примере шлюз приложений обслуживает трафик веб-сайта contoso.com с помощью двух пулов тыловых серверов: пула серверов для видео и пула серверов для изображений.</span><span class="sxs-lookup"><span data-stu-id="2791a-115">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="2791a-116">Запросы для http://contoso.com/image* направляются в пул серверов образов (pool1), а запросы для http://contoso.com/video* направляются в пул серверов видео (pool2).</span><span class="sxs-lookup"><span data-stu-id="2791a-116">Requests for http://contoso.com/image* are routed to image server pool (pool1), and http://contoso.com/video* are routed to video server pool (pool2).</span></span> <span data-ttu-id="2791a-117">Если ни один из шаблонов пути не подходит, выбирается пул серверов по умолчанию (pool1).</span><span class="sxs-lookup"><span data-stu-id="2791a-117">if none of the path patterns match, a default server pool (pool1) is selected.</span></span>

![Маршрут URL-адреса](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="2791a-119">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2791a-119">Before you begin</span></span>

1. <span data-ttu-id="2791a-120">Установите последнюю версию командлетов Azure PowerShell, используя установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="2791a-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="2791a-121">Скачать и установить последнюю версию вы можете в разделе **Windows PowerShell** на [странице загрузок](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2791a-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="2791a-122">Создайте виртуальную сеть и подсеть для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="2791a-123">Убедитесь, что подсеть не используется виртуальной машиной или облачным развертыванием.</span><span class="sxs-lookup"><span data-stu-id="2791a-123">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="2791a-124">Сам шлюз приложений должен находиться в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="2791a-124">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="2791a-125">Для использования шлюза приложений существующие серверы или серверы, для которых в виртуальной сети созданы конечные точки либо же назначен общедоступный или виртуальный IP-адрес, добавляются в пул тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="2791a-125">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="2791a-126">Что необходимо для создания шлюза приложений?</span><span class="sxs-lookup"><span data-stu-id="2791a-126">What is required to create an application gateway?</span></span>

* <span data-ttu-id="2791a-127">**Внутренний пул серверов**. Список IP-адресов внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="2791a-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="2791a-128">Указанные IP-адреса должны относиться к подсети виртуальной сети либо представлять собой общедоступные или виртуальные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="2791a-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="2791a-129">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="2791a-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="2791a-130">Эти параметры привязываются к пулу и применяются ко всем серверам в этом пуле.</span><span class="sxs-lookup"><span data-stu-id="2791a-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="2791a-131">**Интерфейсный порт**. Общедоступный порт, открытый в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="2791a-132">Трафик поступает на этот порт, а затем перенаправляется на один из тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="2791a-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="2791a-133">**Прослушиватель**. У прослушивателя есть интерфейсный порт, протокол (Http или Https — с учетом регистра) и имя SSL-сертификата (в случае настройки разгрузки SSL).</span><span class="sxs-lookup"><span data-stu-id="2791a-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="2791a-134">**Правило**. Правило связывает прослушиватель и внутренний пул серверов, а также определяет, в какой внутренний пул серверов следует направлять трафик, поступающий на определенный прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="2791a-134">**Rule:** The rule binds the listener, the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="2791a-135">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="2791a-135">Create an application gateway</span></span>

<span data-ttu-id="2791a-136">Разница между использованием классической модели развертывания Azure и модели Azure Resource Manager заключается в порядке создания шлюза приложения и элементов, которые нужно настроить.</span><span class="sxs-lookup"><span data-stu-id="2791a-136">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="2791a-137">При использовании Resource Manager все элементы, которые будут включены в единый ресурс шлюза приложений, сначала настраиваются по отдельности.</span><span class="sxs-lookup"><span data-stu-id="2791a-137">With Resource Manager, all items that make an application gateway are configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="2791a-138">Ниже приведены пошаговые инструкции по созданию шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-138">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="2791a-139">Создание группы ресурсов для диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2791a-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="2791a-140">Создание виртуальной сети, подсети и общедоступного IP-адреса для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-140">Create a virtual network, subnet, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="2791a-141">Создание объекта конфигурации шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="2791a-142">Создание ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="2791a-143">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="2791a-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="2791a-144">Убедитесь, что у вас установлена последняя версия Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2791a-144">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="2791a-145">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2791a-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="2791a-146">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="2791a-146">Step 1</span></span>

<span data-ttu-id="2791a-147">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="2791a-147">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="2791a-148">Вам будет предложено указать свои учетные данные для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2791a-148">You are prompted to authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="2791a-149">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="2791a-149">Step 2</span></span>

<span data-ttu-id="2791a-150">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2791a-150">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="2791a-151">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="2791a-151">Step 3</span></span>

<span data-ttu-id="2791a-152">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="2791a-152">Choose which of your Azure subscriptions to use.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="2791a-153">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="2791a-153">Step 4</span></span>

<span data-ttu-id="2791a-154">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="2791a-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="2791a-155">В качестве альтернативы можно также создать теги группы ресурсов для шлюза приложений:</span><span class="sxs-lookup"><span data-stu-id="2791a-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="2791a-156">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="2791a-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="2791a-157">Эта группа ресурсов используется в качестве расположения по умолчанию для всех ресурсов данной группы.</span><span class="sxs-lookup"><span data-stu-id="2791a-157">This resource group is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="2791a-158">Убедитесь, что во всех командах для создания шлюза приложений используется одна группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2791a-158">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="2791a-159">В приведенном выше примере мы создали группу ресурсов с именем appgw-RG и расположением West US (западная часть США).</span><span class="sxs-lookup"><span data-stu-id="2791a-159">In the example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="2791a-160">Если вам нужно настроить пользовательскую пробу для шлюза приложений, ознакомьтесь со статьей [Создание пользовательской проверки для шлюза приложений с помощью PowerShell для диспетчера ресурсов Azure](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2791a-160">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="2791a-161">Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2791a-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="2791a-162">Создание виртуальной сети и подсети для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-162">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="2791a-163">В следующем примере показано создание виртуальной сети с помощью диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2791a-163">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="2791a-164">В этом примере создается виртуальная сеть для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-164">This example creates a VNET for the Application Gateway.</span></span> <span data-ttu-id="2791a-165">Шлюзу приложений требуется собственная подсеть, поэтому эта подсеть меньше, чем адресное пространство виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="2791a-165">Application Gateway requires its own subnet, for this reason the subnet created for the Application Gateway is smaller than the VNET address space.</span></span> <span data-ttu-id="2791a-166">При этом можно настраивать другие ресурсы, включая, помимо прочего, веб-серверы, в той же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="2791a-166">This allows for other resources, including but not limited to web servers to be configured in the same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="2791a-167">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="2791a-167">Step 1</span></span>

<span data-ttu-id="2791a-168">Назначьте диапазон адресов 10.0.0.0/24 переменной подсети, которая будет использоваться для создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="2791a-168">Assign the address range 10.0.0.0/24 to the subnet variable to be used to create a virtual network.</span></span>  <span data-ttu-id="2791a-169">Это действие создает объект конфигурации подсети для шлюза приложений, который используется в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="2791a-169">This creates the subnet configuration object for the Application Gateway, which is used in the next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="2791a-170">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="2791a-170">Step 2</span></span>

<span data-ttu-id="2791a-171">Создайте виртуальную сеть с именем **appgwvnet** в группе ресурсов **appgw-rg** для региона "Западная часть США" при помощи префикса 10.0.0.0/16 с подсетью 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="2791a-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="2791a-172">Это действие завершает настройку виртуальной сети с одной подсетью для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-172">This completes the configuration of the VNET with a single subnet for the Application Gateway to reside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="2791a-173">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="2791a-173">Step 3</span></span>

<span data-ttu-id="2791a-174">Назначьте переменную для подсети, которая будет использоваться далее. Эта переменная будет передана в командлет `New-AzureRMApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="2791a-174">Assign the subnet variable for the next steps, this is passed to the `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="2791a-175">Создание общедоступного IP-адреса для конфигурации интерфейсной части</span><span class="sxs-lookup"><span data-stu-id="2791a-175">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="2791a-176">Создайте ресурс общедоступного IP-адреса с именем **publicIP01** в группе ресурсов **appgw-rg** для региона "Западная часть США".</span><span class="sxs-lookup"><span data-stu-id="2791a-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="2791a-177">Чтобы получать запросы для балансировки нагрузки, шлюз приложений может использовать общедоступный IP-адрес, внутренний IP-адрес или сразу оба.</span><span class="sxs-lookup"><span data-stu-id="2791a-177">Application Gateway can use a public IP address, internal IP address or both to receive requests for load balancing.</span></span>  <span data-ttu-id="2791a-178">В этом примере используется общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="2791a-178">This example only uses a public IP address.</span></span> <span data-ttu-id="2791a-179">В следующем примере для создания общего IP-адреса DNS-имя не настраивается.</span><span class="sxs-lookup"><span data-stu-id="2791a-179">In the following example, no DNS name is configured for creating the Public IP address.</span></span>  <span data-ttu-id="2791a-180">Шлюз приложений не поддерживает пользовательские DNS-имена в общедоступных IP-адресах.</span><span class="sxs-lookup"><span data-stu-id="2791a-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="2791a-181">Если для общедоступной конечной точки требуется пользовательское имя, необходимо создать запись CNAME, указывающую на автоматически созданное DNS-имя для общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="2791a-181">If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="2791a-182">IP-адрес назначается шлюзу приложений при запуске службы.</span><span class="sxs-lookup"><span data-stu-id="2791a-182">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="2791a-183">Создание конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="2791a-183">Create application gateway configuration</span></span>

<span data-ttu-id="2791a-184">Перед созданием шлюза приложений необходимо настроить все элементы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2791a-184">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="2791a-185">В ходе следующих шагов создаются необходимые элементы конфигурации для ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-185">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="2791a-186">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="2791a-186">Step 1</span></span>

<span data-ttu-id="2791a-187">Создайте конфигурацию IP-адресов шлюза приложений с именем **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="2791a-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="2791a-188">При запуске шлюз приложений получает IP-адрес из настроенной подсети. Затем шлюз маршрутизирует сетевой трафик на IP-адреса из внутреннего пула IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="2791a-188">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="2791a-189">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="2791a-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="2791a-190">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="2791a-190">Step 2</span></span>

<span data-ttu-id="2791a-191">Настройте для внутренних пулов IP-адресов **pool01** и **pool2** IP-адреса **pool1** и **pool2**.</span><span class="sxs-lookup"><span data-stu-id="2791a-191">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="2791a-192">Эти IP-адреса являются IP-адресами ресурсов, где размещается веб-приложение, которое будет защищено с помощью шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-192">These IP addresses are the IP addresses of the resources that are hosting the web application to be protected by the application gateway.</span></span> <span data-ttu-id="2791a-193">Работоспособность этих участников серверного пула проверяется с помощью базовых или пользовательских проб.</span><span class="sxs-lookup"><span data-stu-id="2791a-193">These backend pool members are all validated to be healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="2791a-194">Затем при поступлении запросов в шлюз приложений к ним перенаправляется трафик.</span><span class="sxs-lookup"><span data-stu-id="2791a-194">Traffic is then routed to them when requests come into the application gateway.</span></span> <span data-ttu-id="2791a-195">Серверные пулы могут использоваться несколькими правилами в шлюзе приложений. Это означает, что один серверный пул может использоваться для нескольких веб-приложений, которые находятся на том же узле.</span><span class="sxs-lookup"><span data-stu-id="2791a-195">Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="2791a-196">В этом примере используются два пула тыловых серверов для маршрутизации сетевого трафика на основе URL-пути.</span><span class="sxs-lookup"><span data-stu-id="2791a-196">In this example, there are two back-end pools to route network traffic based on the URL path.</span></span> <span data-ttu-id="2791a-197">Один пул принимает трафик для URL-пути /video, а другой — для пути /image.</span><span class="sxs-lookup"><span data-stu-id="2791a-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="2791a-198">Замените приведенные выше IP-адреса и добавьте IP-адреса конечных точек своего приложения.</span><span class="sxs-lookup"><span data-stu-id="2791a-198">Replace the preceding IP addresses to add your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="2791a-199">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="2791a-199">Step 3</span></span>

<span data-ttu-id="2791a-200">Настройте параметры шлюзов приложений **poolsetting01** и **poolsetting02** для балансировки нагрузки сетевого трафика во внутреннем пуле.</span><span class="sxs-lookup"><span data-stu-id="2791a-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="2791a-201">В этом примере вы настроите различные параметры пулов тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="2791a-201">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="2791a-202">Для каждого пула тыловых серверов параметры можно настроить отдельно.</span><span class="sxs-lookup"><span data-stu-id="2791a-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="2791a-203">Серверные параметры HTTP используются правилами для перенаправления трафика соответствующим участникам серверного пула.</span><span class="sxs-lookup"><span data-stu-id="2791a-203">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="2791a-204">Они определяют протокол и порт, используемый для отправки трафика участникам серверного пула.</span><span class="sxs-lookup"><span data-stu-id="2791a-204">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="2791a-205">Сеансы на основе файлов cookie также определяются с помощью серверных параметров HTTP.</span><span class="sxs-lookup"><span data-stu-id="2791a-205">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="2791a-206">Если этот параметр включен, соответствие сеансу на основе файлов cookie отправляет для каждого пакета трафик в ту же серверную часть, что и для предыдущих запросов.</span><span class="sxs-lookup"><span data-stu-id="2791a-206">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="2791a-207">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="2791a-207">Step 4</span></span>

<span data-ttu-id="2791a-208">Настройте внешний IP-адрес, используя конечную точку с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="2791a-208">Configure the front-end IP with public IP endpoint.</span></span> <span data-ttu-id="2791a-209">Объект конфигурации внешнего IP-адреса используется прослушивателем для соотношения внешнего IP-адреса с прослушивателем.</span><span class="sxs-lookup"><span data-stu-id="2791a-209">The front-end IP configuration object is used by a listener to relate the outward facing IP address with the listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="2791a-210">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="2791a-210">Step 5</span></span>

<span data-ttu-id="2791a-211">Настройте внешний порт для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-211">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="2791a-212">Объект конфигурации интерфейсного порта используется прослушивателем для определения порта, на котором шлюз приложений прослушивает трафик, поступающий в прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="2791a-212">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="2791a-213">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="2791a-213">Step 6</span></span>

<span data-ttu-id="2791a-214">Создайте прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="2791a-214">Configure the listener.</span></span> <span data-ttu-id="2791a-215">Этот шаг позволяет настроить прослушиватель для общедоступного IP-адреса и порта, используемых для получения входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="2791a-215">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="2791a-216">В следующем примере используются ранее настроенная внешняя IP-конфигурация, конфигурация интерфейсных портов и протокол (HTTP или HTTPS) и настраивается прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="2791a-216">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="2791a-217">В этом примере прослушиватель прослушивает трафик HTTP через порт 80 для общедоступного IP-адреса, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="2791a-217">In this example, the listener listens to HTTP traffic on port 80 on the public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="2791a-218">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="2791a-218">Step 7</span></span>

<span data-ttu-id="2791a-219">Настройте пути URL-правил для пулов тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="2791a-219">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="2791a-220">На этом этапе настраивается относительный путь, который шлюз приложений использует для сопоставления URL-пути с внутренним пулом, который назначается для обработки входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="2791a-220">This step configures the relative path used by application gateway and defines the mapping between the URL path and the back-end pool that is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2791a-221">Каждый путь должен начинаться с косой черты (/). Знак "\*" может находиться только в конце.</span><span class="sxs-lookup"><span data-stu-id="2791a-221">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="2791a-222">Примеры допустимых значений: /xyz, /xyz* или /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="2791a-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="2791a-223">Строка, передаваемая для сопоставления пути, не должна содержать никакого текста после первого символа "?" или "#", и сами эти символы не допускаются.</span><span class="sxs-lookup"><span data-stu-id="2791a-223">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="2791a-224">В следующем примере создаются два правила: одно для пути маршрутизации трафика /image во внутренний пул pool1, а другое для пути маршрутизации трафика /video во внутренний пул pool2.</span><span class="sxs-lookup"><span data-stu-id="2791a-224">The following example creates two rules: one for "/image/" path routing traffic to back-end "pool1" and another one for "/video/" path routing traffic to back-end "pool2."</span></span> <span data-ttu-id="2791a-225">Эти правила гарантируют, что трафик для каждого набора URL-адресов направляется к серверной части.</span><span class="sxs-lookup"><span data-stu-id="2791a-225">These rules ensure that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="2791a-226">Например, файл http://contoso.com/image/figure1.jpg передается в pool1, а http://contoso.com/video/example.mp4 — в pool2.</span><span class="sxs-lookup"><span data-stu-id="2791a-226">For example, http://contoso.com/image/figure1.jpg goes to pool1 and http://contoso.com/video/example.mp4 goes to pool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="2791a-227">При настройке сопоставления для пути правил также настраивается пул серверной части по умолчанию, который будет использоваться, если путь не соответствует ни одному из предустановленных правил.</span><span class="sxs-lookup"><span data-stu-id="2791a-227">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="2791a-228">Например, файл http://contoso.com/shoppingcart/test.html передается в pool1, так как этот пул определен как пул по умолчанию для несоответствующего трафика.</span><span class="sxs-lookup"><span data-stu-id="2791a-228">For example, http://contoso.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="2791a-229">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="2791a-229">Step 8</span></span>

<span data-ttu-id="2791a-230">Создайте параметр правила.</span><span class="sxs-lookup"><span data-stu-id="2791a-230">Create a rule setting.</span></span> <span data-ttu-id="2791a-231">Этот шаг позволяет настроить шлюз приложений для маршрутизации на основе URL-путей.</span><span class="sxs-lookup"><span data-stu-id="2791a-231">This step configures the application gateway to use URL path-based routing.</span></span> <span data-ttu-id="2791a-232">Определенная ранее переменная `$urlPathMap` теперь используется для создания правила на основе пути.</span><span class="sxs-lookup"><span data-stu-id="2791a-232">The `$urlPathMap` variable defined in the earlier step is now used to create the path-based rule.</span></span> <span data-ttu-id="2791a-233">На этом шаге мы связываем правило с прослушивателем и сопоставлением URL-пути, созданным ранее.</span><span class="sxs-lookup"><span data-stu-id="2791a-233">In this step, we associate the rule with a listener and the url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="2791a-234">Шаг 9.</span><span class="sxs-lookup"><span data-stu-id="2791a-234">Step 9</span></span>

<span data-ttu-id="2791a-235">Настройте количество экземпляров и размер шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-235">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="2791a-236">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="2791a-236">Create Application Gateway</span></span>

<span data-ttu-id="2791a-237">Создайте шлюз приложений со всеми объектами конфигурации, описанными выше.</span><span class="sxs-lookup"><span data-stu-id="2791a-237">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="2791a-238">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="2791a-238">Get application gateway DNS name</span></span>

<span data-ttu-id="2791a-239">После создания шлюза следует настроить внешний интерфейс для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="2791a-239">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="2791a-240">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="2791a-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="2791a-241">Чтобы гарантировать попадание пользователей на шлюз приложений, можно использовать запись CNAME, чтобы указать общедоступную конечную точку шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-241">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="2791a-242">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2791a-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="2791a-243">Чтобы настроить запись CNAME интерфейсного IP-адреса, получите сведения о шлюзе приложений и соответствующее IP- или DNS-имя с помощью элемента PublicIPAddress, связанного со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="2791a-243">To configure the frontend IP CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="2791a-244">DNS-имя шлюза приложений следует использовать для создания записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="2791a-244">The application gateway's DNS name should be used to create a CNAME record.</span></span> <span data-ttu-id="2791a-245">Использование записи A не рекомендуется, так как виртуальный IP-адрес может измениться после перезапуска приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="2791a-245">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2791a-246">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2791a-246">Next steps</span></span>

<span data-ttu-id="2791a-247">Информацию о разгрузке SSL см. в статье о [настройке шлюза приложений для разгрузки SSL](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2791a-247">If you want to learn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

