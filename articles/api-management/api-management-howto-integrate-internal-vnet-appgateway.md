---
title: "Как использовать службу управления API Azure в виртуальных сетях со шлюзом приложений | Документация Майкрософт"
description: "Узнайте, как установить и настроить службу управления API Azure во внутренней виртуальной сети с интерфейсным шлюзом приложений (WAF)"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 8131ded6b74e9c544bf70b1a4659ed07e5def04d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="6c33c-103">Интеграция службы управления API во внутреннюю сеть со шлюзом приложений</span><span class="sxs-lookup"><span data-stu-id="6c33c-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="6c33c-104"><a name="overview"> </a> Обзор</span><span class="sxs-lookup"><span data-stu-id="6c33c-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="6c33c-105">Если настроить службу управления API для работы в виртуальной сети в режиме внутренней сети, она будет доступна только из этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c33c-105">The API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within the Virtual Network.</span></span> <span data-ttu-id="6c33c-106">Шлюз приложений Azure — это служба PaaS, выполняющая функции подсистемы балансировки нагрузки на сетевом уровне 7.</span><span class="sxs-lookup"><span data-stu-id="6c33c-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="6c33c-107">Это служба обратного прокси-сервера, которая содержит также брандмауэр веб-приложения (WAF).</span><span class="sxs-lookup"><span data-stu-id="6c33c-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="6c33c-108">Объединяя возможности службы управления API, работающей во внутренней виртуальной сети, и интерфейса шлюза приложений, вы можете реализовать следующие сценарии.</span><span class="sxs-lookup"><span data-stu-id="6c33c-108">Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:</span></span>

* <span data-ttu-id="6c33c-109">Использовать один ресурс управления API одновременно и для внешних, и для внутренних потребителей.</span><span class="sxs-lookup"><span data-stu-id="6c33c-109">Use the same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="6c33c-110">Использовать один ресурс управления API, определив для него в службе управления API подмножество API-интерфейсов, доступных для внешних потребителей.</span><span class="sxs-lookup"><span data-stu-id="6c33c-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="6c33c-111">Создать простой способ включать и отключать доступ из Интернета к управлению API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-111">Provide a turn-key way to switch access to API Management from the public Internet on and off.</span></span> 

##<span data-ttu-id="6c33c-112"><a name="scenario"> </a> Сценарий</span><span class="sxs-lookup"><span data-stu-id="6c33c-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="6c33c-113">В этой статье мы рассмотрим, как можно использовать одну службу управления API одновременно для внутренних и внешних потребителей, а также как сделать ее единым интерфейсным компонентом для локальных и облачных API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-113">This article will cover how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="6c33c-114">Также вы узнаете, как предоставить некоторое подмножество этих API-интерфейсов (в нашем примере они выделены зеленым цветом) для внешнего использования, применив функцию шлюза приложений PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="6c33c-114">You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using the PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="6c33c-115">В первом примере конфигурации все API-интерфейсы управляются только из виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c33c-115">In the first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="6c33c-116">Внутренние потребители (выделены оранжевым цветом) могут обращаться ко всем внутренним и внешним API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="6c33c-117">Так трафик никогда не выходит в Интернет, а благодаря каналам Express Route достигается высокая производительность.</span><span class="sxs-lookup"><span data-stu-id="6c33c-117">Traffic never goes out to Internet a high performance is delivered via Express Route circuits.</span></span>

![Маршрут URL-адреса](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="6c33c-119"><a name="before-you-begin"> </a> Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="6c33c-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="6c33c-120">Установите последнюю версию командлетов Azure PowerShell, используя установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="6c33c-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="6c33c-121">Последнюю версию можно загрузить и установить в разделе **Windows PowerShell** на [странице загрузок](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6c33c-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="6c33c-122">Создайте виртуальную сеть и отдельные подсети в ней для службы управления API и шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6c33c-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="6c33c-123">Если вы планируете создавать пользовательские DNS-серверы для виртуальной сети, сделайте это перед началом развертывания.</span><span class="sxs-lookup"><span data-stu-id="6c33c-123">If you intend to create a custom DNS server for the Virtual Network, do so before starting the deployment.</span></span> <span data-ttu-id="6c33c-124">Проверьте, все ли работает правильно. Виртуальная машина, созданная в новой подсети этой виртуальной сети, должна разрешать адреса всех конечных точек службы Azure и обращаться к ним.</span><span class="sxs-lookup"><span data-stu-id="6c33c-124">Double check it works by ensuring a virtual machine created in a new subnet in the Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-to-create-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="6c33c-125">Что нужно для того, чтобы интегрировать управление API со шлюзом приложений?</span><span class="sxs-lookup"><span data-stu-id="6c33c-125">What is required to create an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="6c33c-126">**Пул тыловых серверов**. Это внутренний виртуальный IP-адрес службы управления API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-126">**Back-end server pool:** This is the internal virtual IP address of the API Management service.</span></span>
* <span data-ttu-id="6c33c-127">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="6c33c-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="6c33c-128">Эти параметры применяются ко всем серверам в этом пуле.</span><span class="sxs-lookup"><span data-stu-id="6c33c-128">These settings are applied to all servers within the pool.</span></span>
* <span data-ttu-id="6c33c-129">**Внешний порт**. Общедоступный порт, открытый в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="6c33c-129">**Front-end port:** This is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="6c33c-130">Трафик, поступающий на этот порт, перенаправляется на один из тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="6c33c-130">Traffic hitting it gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="6c33c-131">**Прослушиватель**. У прослушивателя есть интерфейсный порт, протокол (Http или Https — с учетом регистра) и имя SSL-сертификата (в случае настройки разгрузки SSL).</span><span class="sxs-lookup"><span data-stu-id="6c33c-131">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="6c33c-132">**Правило**. Это правило связывает прослушиватель с пулом тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="6c33c-132">**Rule:** The rule binds a listener to a back-end server pool.</span></span>
* <span data-ttu-id="6c33c-133">**Пользовательские проверки работоспособности**. Шлюз приложений по умолчанию использует проверки на основе IP-адреса, чтобы найти активные серверы в пуле BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="6c33c-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active.</span></span> <span data-ttu-id="6c33c-134">Служба управления API отвечает только на те запросы, которые имеют правильный заголовок узла, поэтому стандартные проверки завершаются ошибкой.</span><span class="sxs-lookup"><span data-stu-id="6c33c-134">The API Management service only responds to requests which have the correct host header, hence the default probes fail.</span></span> <span data-ttu-id="6c33c-135">Вам следует определить пользовательскую проверку работоспособности, чтобы шлюз приложений мог определять работоспособность службы и передавать в нее запросы.</span><span class="sxs-lookup"><span data-stu-id="6c33c-135">A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.</span></span>
* <span data-ttu-id="6c33c-136">**Сертификат для пользовательского домена**. Чтобы осуществлять доступ из Интернета в службу управления API, создайте сопоставление CNAME, связывающее имя узла с DNS-именем интерфейса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6c33c-136">**Custom domain certificate:** To access API Management from the internet you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name.</span></span> <span data-ttu-id="6c33c-137">Это позволит службе управления API распознавать допустимость заголовка hostname и сертификата, который передан в шлюз приложений и пересылается в управление API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-137">This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="6c33c-138"><a name="overview-steps"> </a> Действия по интеграции управления API со шлюзом приложений</span><span class="sxs-lookup"><span data-stu-id="6c33c-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="6c33c-139">Создание группы ресурсов для диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6c33c-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="6c33c-140">Создание виртуальной сети, подсети и общедоступного IP-адреса для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6c33c-140">Create a Virtual Network, subnet, and public IP for the Application Gateway.</span></span> <span data-ttu-id="6c33c-141">Создайте еще одну подсеть для управления API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="6c33c-142">Создайте службу управления API в той подсети виртуальной сети, которую вы создали ранее. Должен использоваться режим внутренней сети.</span><span class="sxs-lookup"><span data-stu-id="6c33c-142">Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.</span></span>
4. <span data-ttu-id="6c33c-143">Настройте пользовательское доменное имя в службе управления API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-143">Setup the custom domain name in the API Management service.</span></span>
5. <span data-ttu-id="6c33c-144">Создайте объект конфигурации шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6c33c-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="6c33c-145">Создайте ресурс шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6c33c-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="6c33c-146">Создайте сопоставление CNAME, связывающее DNS-имя шлюза приложений с именем узла прокси-сервера управления API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-146">Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="6c33c-147">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="6c33c-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="6c33c-148">Убедитесь, что у вас установлена последняя версия Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c33c-148">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="6c33c-149">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6c33c-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="6c33c-150">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="6c33c-150">Step 1</span></span>

<span data-ttu-id="6c33c-151">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="6c33c-151">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="6c33c-152">Выполните аутентификацию со своими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="6c33c-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="6c33c-153">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="6c33c-153">Step 2</span></span>

<span data-ttu-id="6c33c-154">Проверьте и выберите подписки для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6c33c-154">Check the subscriptions for the account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="6c33c-155">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="6c33c-155">Step 3</span></span>

<span data-ttu-id="6c33c-156">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="6c33c-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="6c33c-157">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="6c33c-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="6c33c-158">Оно используется в качестве расположения по умолчанию для всех ресурсов данной группы.</span><span class="sxs-lookup"><span data-stu-id="6c33c-158">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="6c33c-159">Убедитесь, что во всех командах для создания шлюза приложений используется одна группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6c33c-159">Make sure that all commands to create an application gateway use the same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="6c33c-160">Создание виртуальной сети и подсети для шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="6c33c-160">Create a Virtual Network and a subnet for the application gateway</span></span>

<span data-ttu-id="6c33c-161">В следующем примере показано создание виртуальной сети с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6c33c-161">The following example shows how to create a Virtual Network using the resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="6c33c-162">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="6c33c-162">Step 1</span></span>

<span data-ttu-id="6c33c-163">Создайте переменную подсети с диапазоном адресов 10.0.0.0/24, которая будет использоваться для шлюза приложений при создании виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c33c-163">Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="6c33c-164">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="6c33c-164">Step 2</span></span>

<span data-ttu-id="6c33c-165">Создайте переменную подсети с диапазоном адресов 10.0.1.0/24, которая будет использоваться для управления API при создании виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c33c-165">Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="6c33c-166">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="6c33c-166">Step 3</span></span>

<span data-ttu-id="6c33c-167">Создайте виртуальную сеть с именем **appgwvnet** в группе ресурсов **apim-appGw-RG** для региона "Западная часть США", назначив ей префикс 10.0.0.0/16. Создайте в ней подсети 10.0.0.0/24 и 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="6c33c-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region using the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="6c33c-168">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="6c33c-168">Step 4</span></span>

<span data-ttu-id="6c33c-169">Назначьте переменную для подсети, которая будет использоваться далее.</span><span class="sxs-lookup"><span data-stu-id="6c33c-169">Assign a subnet variable for the next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="6c33c-170">Создание службы управления API в виртуальной сети, настроенной в режиме внутренней сети</span><span class="sxs-lookup"><span data-stu-id="6c33c-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="6c33c-171">В следующем примере демонстрируется создание службы управления API в виртуальной сети, настроенной только для внутреннего доступа.</span><span class="sxs-lookup"><span data-stu-id="6c33c-171">The following example shows how to create an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="6c33c-172">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="6c33c-172">Step 1</span></span>
<span data-ttu-id="6c33c-173">Создайте объект виртуальной сети для управления API, используя созданную выше переменную подсети $apimsubnetdata.</span><span class="sxs-lookup"><span data-stu-id="6c33c-173">Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="6c33c-174">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="6c33c-174">Step 2</span></span>
<span data-ttu-id="6c33c-175">Создайте службу управления API в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c33c-175">Create an API Management service inside the Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="6c33c-176">Когда завершится выполнение предыдущей команды, выполните инструкции из раздела [DNS Configuration ](api-management-using-with-internal-vnet.md#apim-dns-configuration) (Настройка DNS) для доступа к службе управления API во внутренней виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c33c-176">After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="6c33c-177">Настройка пользовательского доменного имени в службе управления API</span><span class="sxs-lookup"><span data-stu-id="6c33c-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="6c33c-178">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="6c33c-178">Step 1</span></span>
<span data-ttu-id="6c33c-179">Отправьте сертификат с закрытым ключом для домена.</span><span class="sxs-lookup"><span data-stu-id="6c33c-179">Upload the certificate with private key for the domain.</span></span> <span data-ttu-id="6c33c-180">В нашем примере это `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="6c33c-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path to .pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="6c33c-181">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="6c33c-181">Step 2</span></span>
<span data-ttu-id="6c33c-182">Отправив сертификат, создайте объект конфигурации имени узла для прокси-сервера с именем узла `api.contoso.net`. Имя должно быть именно в домене `*.contoso.net`, на который предоставляет права этот сертификат.</span><span class="sxs-lookup"><span data-stu-id="6c33c-182">Once the certificate is uploaded, create a hostname configuration object for the proxy with a hostname of `api.contoso.net`, as the example certificate provides authority for the  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="6c33c-183">Создание общедоступного IP-адреса для конфигурации интерфейсной части</span><span class="sxs-lookup"><span data-stu-id="6c33c-183">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="6c33c-184">Создайте ресурс общедоступного IP-адреса с именем **publicIP01** в группе ресурсов **apim-appGw-RG** для региона "Западная часть США".</span><span class="sxs-lookup"><span data-stu-id="6c33c-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="6c33c-185">IP-адрес назначается шлюзу приложений при запуске службы.</span><span class="sxs-lookup"><span data-stu-id="6c33c-185">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="6c33c-186">Создание конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="6c33c-186">Create application gateway configuration</span></span>

<span data-ttu-id="6c33c-187">Перед созданием шлюза приложений необходимо настроить все элементы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6c33c-187">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="6c33c-188">В ходе следующих шагов создаются необходимые элементы конфигурации для ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6c33c-188">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="6c33c-189">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="6c33c-189">Step 1</span></span>

<span data-ttu-id="6c33c-190">Создайте конфигурацию IP-адресов шлюза приложений с именем **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="6c33c-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="6c33c-191">При запуске шлюз приложений получает IP-адрес из настроенной подсети. Затем шлюз маршрутизирует сетевой трафик на IP-адреса из внутреннего пула IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="6c33c-191">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="6c33c-192">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="6c33c-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="6c33c-193">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="6c33c-193">Step 2</span></span>

<span data-ttu-id="6c33c-194">Настройте интерфейсный порт IP для конечной точки с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="6c33c-194">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="6c33c-195">Это порт, к которому подключаются пользователи.</span><span class="sxs-lookup"><span data-stu-id="6c33c-195">This port is the port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="6c33c-196">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="6c33c-196">Step 3</span></span>

<span data-ttu-id="6c33c-197">Настройте внешний IP-адрес, используя конечную точку с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="6c33c-197">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="6c33c-198">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="6c33c-198">Step 4</span></span>

<span data-ttu-id="6c33c-199">Настройте в шлюзе приложений сертификат для шифрования и расшифровки проходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="6c33c-199">Configure the certificate for the Application Gateway, used to decrypt and re-encrypt the traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="6c33c-200">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="6c33c-200">Step 5</span></span>

<span data-ttu-id="6c33c-201">Создайте прослушиватель HTTP для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6c33c-201">Create the HTTP listener for the Application Gateway.</span></span> <span data-ttu-id="6c33c-202">Назначьте для внешнего интерфейса параметры IP-адресов, порт и сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="6c33c-202">Assign the front-end IP configuration, port, and ssl certificate to it.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="6c33c-203">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="6c33c-203">Step 6</span></span>

<span data-ttu-id="6c33c-204">Создайте пользовательскую проверку для конечной точки `ContosoApi` прокси-сервера службы управления API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-204">Create a custom probe to the API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="6c33c-205">По умолчанию на всех службах управления API для конечной точки проверки работоспособности используется путь `/status-0123456789abcdef`.</span><span class="sxs-lookup"><span data-stu-id="6c33c-205">The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services.</span></span> <span data-ttu-id="6c33c-206">Укажите `api.contoso.net` в качестве имени узла пользовательской пробы, чтобы защитить его с помощью SSL-сертификата.</span><span class="sxs-lookup"><span data-stu-id="6c33c-206">Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="6c33c-207">Когда в общедоступной службе Azure создается служба с именем `contosoapi.azure-api.net`, для ее прокси-сервера по умолчанию назначается имя узла `contosoapi`.</span><span class="sxs-lookup"><span data-stu-id="6c33c-207">The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="6c33c-208">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="6c33c-208">Step 7</span></span>

<span data-ttu-id="6c33c-209">Передайте сертификат, который будет использоваться для ресурсов внутреннего пула, поддерживающих протокол SSL.</span><span class="sxs-lookup"><span data-stu-id="6c33c-209">Upload the certificate to be used on the SSL-enabled backend pool resources.</span></span> <span data-ttu-id="6c33c-210">Это тот же сертификат, который вы указали выше на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="6c33c-210">This is the same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path to .cer file>
```

### <a name="step-8"></a><span data-ttu-id="6c33c-211">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="6c33c-211">Step 8</span></span>

<span data-ttu-id="6c33c-212">Настройте HTTP для внутреннего пула шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6c33c-212">Configure HTTP backend settings for the Application Gateway.</span></span> <span data-ttu-id="6c33c-213">К настройкам относится и предел времени ожидания, по истечении которого запрос к внутренним серверам отменяется.</span><span class="sxs-lookup"><span data-stu-id="6c33c-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="6c33c-214">Это значение отличается от времени ожидания проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="6c33c-214">This value is different from the probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="6c33c-215">Шаг 9.</span><span class="sxs-lookup"><span data-stu-id="6c33c-215">Step 9</span></span>

<span data-ttu-id="6c33c-216">Настройте пул IP-адресов серверной части с именем **apimbackend**, указав для него внутренний виртуальный IP-адрес, созданный ранее для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-216">Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="6c33c-217">Шаг 10</span><span class="sxs-lookup"><span data-stu-id="6c33c-217">Step 10</span></span>

<span data-ttu-id="6c33c-218">Создайте параметры для фиктивного (несуществующего) внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="6c33c-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="6c33c-219">Запросы к путям API, к которым вы не хотите предоставлять доступ из управления API через шлюз приложений, будут попадать на этот внутренний пул и возвращать ошибку 404.</span><span class="sxs-lookup"><span data-stu-id="6c33c-219">Requests to API paths that we do not want to expose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="6c33c-220">Настройте параметры HTTP для внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="6c33c-220">Configure HTTP settings for the dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="6c33c-221">Настройте фиктивный внутренний пул **dummyBackendPool**, который указывает на адрес полного доменного имени **dummybackend.com**. Этот адрес полного доменного имени не существует в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c33c-221">Configure a dummy backend **dummyBackendPool**, which points to a FQDN address **dummybackend.com**. This FQDN address does not exist in the virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="6c33c-222">Создайте параметр правила, который шлюз приложений будет использовать по умолчанию и который указывает на несуществующий внутренний пул **dummybackend.com** в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c33c-222">Create a rule setting that the Application Gateway will use by default which points to the non-existent backend **dummybackend.com** in the Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="6c33c-223">Шаг 11</span><span class="sxs-lookup"><span data-stu-id="6c33c-223">Step 11</span></span>

<span data-ttu-id="6c33c-224">Настройте пути URL-правил для пулов тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="6c33c-224">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="6c33c-225">Это позволяет выбрать некоторое подмножество интерфейсов API из управления API, чтобы открыть к ним общий доступ.</span><span class="sxs-lookup"><span data-stu-id="6c33c-225">This enables selecting only some of the APIs from API Management for being exposed to the public.</span></span> <span data-ttu-id="6c33c-226">Например, из набора `Echo API` (/echo/), `Calculator API` (/calc/) и т. д. сделать доступным из Интернета только `Echo API`.</span><span class="sxs-lookup"><span data-stu-id="6c33c-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="6c33c-227">В следующем примере создается простое правило для маршрутизации трафика от пути /echo/ к пулу тыловых серверов apimProxyBackendPool.</span><span class="sxs-lookup"><span data-stu-id="6c33c-227">The following example creates a simple rule for the "/echo/" path routing traffic to the back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="6c33c-228">Если путь не соответствует правилам, которые необходимо включить с помощью управления API, то при настройке сопоставления для пути правил также настраивается внутренний пул адресов по умолчанию с именем **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="6c33c-228">If the path doesn't match the path rules we want to enable from API Management, the rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="6c33c-229">Например, файл http://api.contoso.net/calc/* перейдет в **dummyBackendPool**, так как этот пул определен как пул по умолчанию для несоответствующего трафика.</span><span class="sxs-lookup"><span data-stu-id="6c33c-229">For example, http://api.contoso.net/calc/* goes to **dummyBackendPool** as it is defined as the default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="6c33c-230">Предыдущий шаг нужен для того, чтобы через шлюз приложений проходили запросы только для пути /echo.</span><span class="sxs-lookup"><span data-stu-id="6c33c-230">The above step ensures that only requests for the path "/echo" are allowed through the Application Gateway.</span></span> <span data-ttu-id="6c33c-231">В ответ на запросы из Интернета на другие API-интерфейсы, настроенные в управлении API, шлюз приложений будет возвращать ошибки 404.</span><span class="sxs-lookup"><span data-stu-id="6c33c-231">Requests to other APIs configured in API Management will throw 404 errors from Application Gateway when accessed from the Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="6c33c-232">Шаг 12</span><span class="sxs-lookup"><span data-stu-id="6c33c-232">Step 12</span></span>

<span data-ttu-id="6c33c-233">Создайте правило для использования маршрутизации на основе URL-путей в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="6c33c-233">Create a rule setting for the Application Gateway to use URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="6c33c-234">Шаг 13</span><span class="sxs-lookup"><span data-stu-id="6c33c-234">Step 13</span></span>

<span data-ttu-id="6c33c-235">Настройте число экземпляров и размер шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="6c33c-235">Configure the number of instances and size for the Application Gateway.</span></span> <span data-ttu-id="6c33c-236">Здесь мы используем [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) для повышения уровня безопасности ресурса управления API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-236">Here we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="6c33c-237">Шаг 14</span><span class="sxs-lookup"><span data-stu-id="6c33c-237">Step 14</span></span>

<span data-ttu-id="6c33c-238">Настройте WAF в режиме предотвращения.</span><span class="sxs-lookup"><span data-stu-id="6c33c-238">Configure WAF to be in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="6c33c-239">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="6c33c-239">Create Application Gateway</span></span>

<span data-ttu-id="6c33c-240">Создайте шлюз приложений, используя все созданные ранее объекты конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6c33c-240">Create an Application Gateway with all the configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-the-api-management-proxy-hostname-to-the-public-dns-name-of-the-application-gateway-resource"></a><span data-ttu-id="6c33c-241">Создание сопоставления CNAME для связи имени узла прокси-сервера управления API с общедоступным DNS-именем ресурса шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="6c33c-241">CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource</span></span>

<span data-ttu-id="6c33c-242">После создания шлюза следует настроить внешний интерфейс для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="6c33c-242">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="6c33c-243">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое имя DNS, которое может быть неудобным для использования.</span><span class="sxs-lookup"><span data-stu-id="6c33c-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use.</span></span> 

<span data-ttu-id="6c33c-244">Для DNS-имени шлюза приложений следует создать запись CNAME, которая будет связывать имя узла прокси-сервера (в примере выше это `api.contoso.net`) с этим DNS-именем.</span><span class="sxs-lookup"><span data-stu-id="6c33c-244">The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name.</span></span> <span data-ttu-id="6c33c-245">Чтобы настроить запись CNAME интерфейсного IP-адреса, получите сведения о шлюзе приложений и соответствующее IP- или DNS-имя с помощью элемента PublicIPAddress.</span><span class="sxs-lookup"><span data-stu-id="6c33c-245">To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element.</span></span> <span data-ttu-id="6c33c-246">Мы не рекомендуем использовать записи типа A, так как виртуальный IP-адрес может измениться после перезапуска шлюза.</span><span class="sxs-lookup"><span data-stu-id="6c33c-246">The use of A-records is not recommended since the VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="6c33c-247"><a name="summary"> </a> Сводка</span><span class="sxs-lookup"><span data-stu-id="6c33c-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="6c33c-248">Служба управления API Azure, настроенная в виртуальной сети, предоставляет свой шлюз в качестве единого интерфейса для всех настроенных API-интерфейсов, как локальных, так и облачных.</span><span class="sxs-lookup"><span data-stu-id="6c33c-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud.</span></span> <span data-ttu-id="6c33c-249">Интеграция шлюза приложений с управлением API дает вам дополнительную гибкость, позволяя избирательно предоставлять доступ к API-интерфейсам через Интернет. Также вы можете использовать брандмауэр веб-приложения в качестве интерфейсного компонента для экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="6c33c-249">Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.</span></span>

##<span data-ttu-id="6c33c-250"><a name="next-steps"> </a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c33c-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="6c33c-251">Дополнительные сведения о шлюзе приложений Azure:</span><span class="sxs-lookup"><span data-stu-id="6c33c-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="6c33c-252">Обзор шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="6c33c-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * <span data-ttu-id="6c33c-253">[Application Gateway Web Application Firewall (preview)](../application-gateway/application-gateway-webapplicationfirewall-overview.md) (Брандмауэр веб-приложения шлюза приложений (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="6c33c-253">[Application Gateway Web Application Firewall](../application-gateway/application-gateway-webapplicationfirewall-overview.md)</span></span>
  * [<span data-ttu-id="6c33c-254">Создание шлюза приложений с помощью маршрутизации на основе пути</span><span class="sxs-lookup"><span data-stu-id="6c33c-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="6c33c-255">См. дополнительные сведения о службе управлении API и виртуальных сетях</span><span class="sxs-lookup"><span data-stu-id="6c33c-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="6c33c-256">Использование службы управления API Azure совместно с внутренней виртуальной сетью</span><span class="sxs-lookup"><span data-stu-id="6c33c-256">Using API Management available only within the VNET</span></span>](api-management-using-with-internal-vnet.md)
  * <span data-ttu-id="6c33c-257">[How to use Azure API Management with virtual networks](api-management-using-with-vnet.md) (Использование управления API Azure в виртуальных сетях)</span><span class="sxs-lookup"><span data-stu-id="6c33c-257">[Using API Management in VNET](api-management-using-with-vnet.md)</span></span>
