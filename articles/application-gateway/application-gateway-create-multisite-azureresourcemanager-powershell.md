---
title: "Создание шлюза приложений для размещения нескольких сайтов | Документация Майкрософт"
description: "Эта страница содержит инструкции по созданию и настройке шлюза приложений Azure для размещения нескольких веб-приложений в одном шлюзе."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: d42efa7d359f5c87c14afbfd138328b37c8ae6c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="f84db-103">Создание шлюза приложений для размещения нескольких веб-приложений</span><span class="sxs-lookup"><span data-stu-id="f84db-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f84db-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="f84db-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="f84db-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="f84db-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="f84db-106">Размещение нескольких сайтов позволяет развернуть в одном шлюзе приложений не одно, а несколько веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="f84db-107">Чтобы определить, какой прослушиватель должен принимать трафик, шлюз приложений проверяет наличие заголовка узла во входящем HTTP-запросе.</span><span class="sxs-lookup"><span data-stu-id="f84db-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="f84db-108">Затем прослушиватель направляет трафик в соответствующий внутренний пул согласно определениям правил шлюза.</span><span class="sxs-lookup"><span data-stu-id="f84db-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="f84db-109">В веб-приложениях с поддержкой протокола SSL шлюз приложений использует расширение SNI (указание имени сервера) для выбора соответствующего прослушивателя веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="f84db-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="f84db-110">Как правило, размещение нескольких сайтов используется для балансировки нагрузки запросов к разным веб-доменам между различными внутренними пулами серверов.</span><span class="sxs-lookup"><span data-stu-id="f84db-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="f84db-111">Подобным образом в одном шлюзе приложений можно разместить несколько поддоменов одного корневого домена.</span><span class="sxs-lookup"><span data-stu-id="f84db-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="f84db-112">Сценарий</span><span class="sxs-lookup"><span data-stu-id="f84db-112">Scenario</span></span>

<span data-ttu-id="f84db-113">В следующем примере шлюз приложений обслуживает трафик сайтов contoso.com и fabrikam.com с помощью двух внутренних пулов серверов: contoso и fabrikam.</span><span class="sxs-lookup"><span data-stu-id="f84db-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="f84db-114">Аналогичную конфигурацию можно использовать для размещения таких поддоменов, как app.contoso.com и blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f84db-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="f84db-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="f84db-116">Before you begin</span></span>

1. <span data-ttu-id="f84db-117">Установите последнюю версию командлетов Azure PowerShell, используя установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="f84db-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="f84db-118">Последнюю версию можно загрузить и установить в разделе **Windows PowerShell** на [странице загрузок](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f84db-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f84db-119">Серверы, добавляемые во внутренний пул для использования шлюза приложений, должны находиться в отдельной подсети виртуальной сети, или их конечные точки должны находиться в этой подсети либо иметь назначенный общедоступный или виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f84db-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="f84db-120">Требования</span><span class="sxs-lookup"><span data-stu-id="f84db-120">Requirements</span></span>

* <span data-ttu-id="f84db-121">**Внутренний пул серверов**. Список IP-адресов внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="f84db-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="f84db-122">Указанные IP-адреса должны относиться к подсети виртуальной сети либо представлять собой общедоступные или виртуальные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="f84db-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="f84db-123">Можно также использовать полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="f84db-123">FQDN can also be used.</span></span>
* <span data-ttu-id="f84db-124">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="f84db-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="f84db-125">Эти параметры привязываются к пулу и применяются ко всем серверам в этом пуле.</span><span class="sxs-lookup"><span data-stu-id="f84db-125">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="f84db-126">**Интерфейсный порт**. Общедоступный порт, открытый в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="f84db-127">Трафик поступает на этот порт, а затем перенаправляется на один из тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="f84db-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="f84db-128">**Прослушиватель**. У прослушивателя есть интерфейсный порт, протокол (Http или Https — с учетом регистра) и имя SSL-сертификата (в случае настройки разгрузки SSL).</span><span class="sxs-lookup"><span data-stu-id="f84db-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="f84db-129">Для шлюзов приложений с поддержкой нескольких сайтов также добавляются имя узла и индикаторы SNI.</span><span class="sxs-lookup"><span data-stu-id="f84db-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="f84db-130">**Правило**. Правило связывает прослушиватель и внутренний пул серверов, а также определяет, в какой внутренний пул серверов следует направлять трафик, поступающий на определенный прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="f84db-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="f84db-131">Правила обрабатываются в том порядке, в котором они указаны, а трафик направляется через первое подходящее правило независимо от точности.</span><span class="sxs-lookup"><span data-stu-id="f84db-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="f84db-132">Например, если для одного порта имеется правило с базовым прослушивателем и правило с многосайтовым прослушивателем, для обеспечения правильной работы правило с многосайтовым прослушивателем должно быть указано перед правилом с базовым прослушивателем.</span><span class="sxs-lookup"><span data-stu-id="f84db-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="f84db-133">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="f84db-133">Create an application gateway</span></span>

<span data-ttu-id="f84db-134">Ниже приведены пошаговые инструкции по созданию шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-134">The following are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="f84db-135">Создание группы ресурсов для диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f84db-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="f84db-136">Создание виртуальной сети, подсетей и общедоступного IP-адреса для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-136">Create a virtual network, subnets, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="f84db-137">Создание объекта конфигурации шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="f84db-138">Создание ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="f84db-139">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="f84db-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="f84db-140">Убедитесь, что у вас установлена последняя версия Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f84db-140">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="f84db-141">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f84db-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="f84db-142">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="f84db-142">Step 1</span></span>

<span data-ttu-id="f84db-143">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="f84db-143">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="f84db-144">Вам будет предложено указать свои учетные данные для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f84db-144">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="f84db-145">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="f84db-145">Step 2</span></span>

<span data-ttu-id="f84db-146">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f84db-146">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="f84db-147">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="f84db-147">Step 3</span></span>

<span data-ttu-id="f84db-148">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="f84db-148">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="f84db-149">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="f84db-149">Step 4</span></span>

<span data-ttu-id="f84db-150">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="f84db-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="f84db-151">В качестве альтернативы можно также создать теги группы ресурсов для шлюза приложений:</span><span class="sxs-lookup"><span data-stu-id="f84db-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="f84db-152">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="f84db-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="f84db-153">Это расположение используется в качестве расположения по умолчанию для всех ресурсов данной группы.</span><span class="sxs-lookup"><span data-stu-id="f84db-153">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="f84db-154">Убедитесь, что во всех командах для создания шлюза приложений используется одна группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f84db-154">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="f84db-155">В приведенном выше примере мы создали группу ресурсов **appgw-RG** в расположении **West US** (Западная часть США).</span><span class="sxs-lookup"><span data-stu-id="f84db-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="f84db-156">Если вам нужно настроить пользовательскую пробу для шлюза приложений, ознакомьтесь со статьей [Создание пользовательской проверки для шлюза приложений с помощью PowerShell для диспетчера ресурсов Azure](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f84db-156">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="f84db-157">Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f84db-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="f84db-158">Создание виртуальной сети и подсетей</span><span class="sxs-lookup"><span data-stu-id="f84db-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="f84db-159">В следующем примере показано создание виртуальной сети с помощью диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f84db-159">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="f84db-160">На этом шаге создаются две подсети.</span><span class="sxs-lookup"><span data-stu-id="f84db-160">Two subnets are created in this step.</span></span> <span data-ttu-id="f84db-161">Первая подсеть предназначена для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-161">The first subnet is for the application gateway itself.</span></span> <span data-ttu-id="f84db-162">Шлюзу приложений требуется собственная подсеть для размещения его экземпляров.</span><span class="sxs-lookup"><span data-stu-id="f84db-162">Application gateway requires its own subnet to hold its instances.</span></span> <span data-ttu-id="f84db-163">В этой подсети могут развертываться только другие шлюзы приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="f84db-164">Вторая подсеть используется для размещения внутренних серверов приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-164">The second subnet is used to hold the application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="f84db-165">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="f84db-165">Step 1</span></span>

<span data-ttu-id="f84db-166">Назначьте переменной subnet диапазон адресов 10.0.0.0/24, который будет использоваться для размещения шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="f84db-167">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="f84db-167">Step 2</span></span>

<span data-ttu-id="f84db-168">Назначьте переменной subnet2 диапазон адресов 10.0.1.0/24, который будет использоваться для внутренних пулов.</span><span class="sxs-lookup"><span data-stu-id="f84db-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="f84db-169">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="f84db-169">Step 3</span></span>

<span data-ttu-id="f84db-170">В группе ресурсов **appgw-rg** для региона "West US" (Западная часть США) создайте виртуальную сеть **appgwvnet** с префиксом 10.0.0.0/16 и подсетями 10.0.0.0/24 и 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="f84db-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="f84db-171">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="f84db-171">Step 4</span></span>

<span data-ttu-id="f84db-172">Назначьте переменную подсети для дальнейших этапов создания шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-172">Assign a subnet variable for the next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="f84db-173">Создание общедоступного IP-адреса для конфигурации интерфейсной части</span><span class="sxs-lookup"><span data-stu-id="f84db-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="f84db-174">Создайте ресурс общедоступного IP-адреса с именем **publicIP01** в группе ресурсов **appgw-rg** для региона "Западная часть США".</span><span class="sxs-lookup"><span data-stu-id="f84db-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="f84db-175">IP-адрес назначается шлюзу приложений при запуске службы.</span><span class="sxs-lookup"><span data-stu-id="f84db-175">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="f84db-176">Создание конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="f84db-176">Create application gateway configuration</span></span>

<span data-ttu-id="f84db-177">Перед созданием шлюза приложений необходимо настроить все элементы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f84db-177">You have to set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="f84db-178">В ходе следующих шагов создаются необходимые элементы конфигурации для ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-178">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="f84db-179">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="f84db-179">Step 1</span></span>

<span data-ttu-id="f84db-180">Создайте конфигурацию IP-адресов шлюза приложений с именем **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="f84db-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="f84db-181">При запуске шлюз приложений получает IP-адрес из настроенной подсети, а после шлюз маршрутизирует сетевой трафик на IP-адреса из внутреннего пула IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="f84db-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="f84db-182">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f84db-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="f84db-183">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="f84db-183">Step 2</span></span>

<span data-ttu-id="f84db-184">Настройте для внутренних пулов IP-адресов **pool01** и **pool2** IP-адреса: **134.170.185.46**, **134.170.188.221**, **134.170.185.50** для **pool1** и **134.170.186.46**, **134.170.189.221**, **134.170.186.50** для **pool2**.</span><span class="sxs-lookup"><span data-stu-id="f84db-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="f84db-185">В этом примере используются два пула внутренних серверов для маршрутизации сетевого трафика на основе запрошенного сайта.</span><span class="sxs-lookup"><span data-stu-id="f84db-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span></span> <span data-ttu-id="f84db-186">Один пул принимает трафик от сайта contoso.com, а другой — от сайта fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="f84db-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="f84db-187">Вам необходимо заменить приведенные выше IP-адреса и добавить IP-адреса конечных точек своего приложения.</span><span class="sxs-lookup"><span data-stu-id="f84db-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span></span> <span data-ttu-id="f84db-188">Вместо внутренних IP-адресов для серверных экземпляров можно также использовать общедоступные IP-адреса, полное доменное имя или сетевую карту виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f84db-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="f84db-189">Чтобы указать полные доменные имена, а не IP-адреса, используйте параметр -BackendFQDNs в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f84db-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="f84db-190">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="f84db-190">Step 3</span></span>

<span data-ttu-id="f84db-191">Настройте параметры шлюзов приложений **poolsetting01** и **poolsetting02** для балансировки нагрузки сетевого трафика во внутреннем пуле.</span><span class="sxs-lookup"><span data-stu-id="f84db-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="f84db-192">В этом примере вы настроите различные параметры пулов тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="f84db-192">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="f84db-193">Для каждого пула тыловых серверов параметры можно настроить отдельно.</span><span class="sxs-lookup"><span data-stu-id="f84db-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="f84db-194">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="f84db-194">Step 4</span></span>

<span data-ttu-id="f84db-195">Настройте внешний IP-адрес, используя конечную точку с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="f84db-195">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="f84db-196">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="f84db-196">Step 5</span></span>

<span data-ttu-id="f84db-197">Настройте внешний порт для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-197">Configure the front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="f84db-198">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="f84db-198">Step 6</span></span>

<span data-ttu-id="f84db-199">Настройте два SSL-сертификата для обоих веб-сайтов, которые будут обслуживаться в этом примере.</span><span class="sxs-lookup"><span data-stu-id="f84db-199">Configure two SSL certificates for the two websites we are going to support in this example.</span></span> <span data-ttu-id="f84db-200">Один сертификат предназначен для трафика contoso.com, а другой — для трафика fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="f84db-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span></span> <span data-ttu-id="f84db-201">Это должны быть сертификаты, выданные веб-сайтам центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="f84db-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="f84db-202">Самозаверяющие сертификаты поддерживаются, но их не рекомендуется использовать трафика в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="f84db-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="f84db-203">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="f84db-203">Step 7</span></span>

<span data-ttu-id="f84db-204">Настройте два прослушивателя для пары веб-сайтов в данном примере.</span><span class="sxs-lookup"><span data-stu-id="f84db-204">Configure two listeners for the two web sites in this example.</span></span> <span data-ttu-id="f84db-205">На этом шаге следует настроить прослушиватели для общедоступного IP-адреса, порта и узла, используемых для получения входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="f84db-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span></span> <span data-ttu-id="f84db-206">Параметр HostName необходим для поддержки нескольких сайтов. Ему нужно присвоить имя соответствующего веб-сайта, для которого будет приниматься трафик.</span><span class="sxs-lookup"><span data-stu-id="f84db-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span></span> <span data-ttu-id="f84db-207">Параметру RequireServerNameIndication следует присвоить значение true для веб-сайтов, которым требуется поддержка протокола SSL в сценарии с несколькими узлами.</span><span class="sxs-lookup"><span data-stu-id="f84db-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="f84db-208">Если требуется поддержка протокола SSL, необходимо также указать SSL-сертификат, используемый для защиты трафика этого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f84db-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span></span> <span data-ttu-id="f84db-209">Сочетание параметров прослушивателя FrontendIPConfiguration, FrontendPort и HostName должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="f84db-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span></span> <span data-ttu-id="f84db-210">Каждый прослушиватель может поддерживать один сертификат.</span><span class="sxs-lookup"><span data-stu-id="f84db-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="f84db-211">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="f84db-211">Step 8</span></span>

<span data-ttu-id="f84db-212">Создайте два параметра правила для пары веб-приложений в данном примере.</span><span class="sxs-lookup"><span data-stu-id="f84db-212">Create two rule setting for the two web applications in this example.</span></span> <span data-ttu-id="f84db-213">Правило объединяет прослушиватели, серверные пулы и параметры протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="f84db-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="f84db-214">На этом шаге следует настроить шлюз приложений для использования базового правила маршрутизации для каждого веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="f84db-214">This step configures the application gateway to use Basic routing rule, one for each website.</span></span> <span data-ttu-id="f84db-215">Трафик, передаваемый на каждый веб-сайт, получает настроенный для него прослушиватель, после чего трафик направляется в заданный северный пул с использованием свойств, указанных в BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="f84db-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="f84db-216">Шаг 9.</span><span class="sxs-lookup"><span data-stu-id="f84db-216">Step 9</span></span>

<span data-ttu-id="f84db-217">Настройте количество экземпляров и размер шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-217">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="f84db-218">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="f84db-218">Create application gateway</span></span>

<span data-ttu-id="f84db-219">Создайте шлюз приложений со всеми объектами конфигурации, описанными выше.</span><span class="sxs-lookup"><span data-stu-id="f84db-219">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="f84db-220">Подготовка шлюза приложений — это длительная операция, которая может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="f84db-220">Application Gateway provisioning is a long running operation and may take some time to complete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="f84db-221">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="f84db-221">Get application gateway DNS name</span></span>

<span data-ttu-id="f84db-222">После создания шлюза следует настроить внешний интерфейс для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="f84db-222">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="f84db-223">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="f84db-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="f84db-224">Чтобы гарантировать попадание пользователей на шлюз приложений, можно использовать запись CNAME, чтобы указать общедоступную конечную точку шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="f84db-225">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f84db-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="f84db-226">Получите информацию о шлюзе приложений и соответствующее IP- или DNS-имя с помощью элемента PublicIPAddress, связанного со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="f84db-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="f84db-227">DNS-имя шлюза приложений должно использоваться для создания записи CNAME, указывающей двум веб-приложениям на это DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="f84db-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="f84db-228">Использование записи A не рекомендуется, так как виртуальный IP-адрес может измениться после перезапуска приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="f84db-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f84db-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f84db-229">Next steps</span></span>

<span data-ttu-id="f84db-230">Узнайте, как защитить веб-сайты с помощью [брандмауэра веб-приложения шлюза приложений](application-gateway-webapplicationfirewall-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f84db-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

