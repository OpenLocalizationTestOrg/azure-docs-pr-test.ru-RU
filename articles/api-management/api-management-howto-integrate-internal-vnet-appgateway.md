---
title: "aaaHow toouse управления API Azure в виртуальной сети со шлюзом приложений | Документы Microsoft"
description: "Узнайте, как toosetup и настройка службы управления API Azure в внутреннюю виртуальную сеть с помощью приложения шлюза (WAF) в качестве внешнего интерфейса"
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
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="9a68f-103">Интеграция службы управления API во внутреннюю сеть со шлюзом приложений</span><span class="sxs-lookup"><span data-stu-id="9a68f-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="9a68f-104"><a name="overview"> </a> Обзор</span><span class="sxs-lookup"><span data-stu-id="9a68f-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="9a68f-105">Hello службы управления API можно настроить в виртуальной сети в режиме внутренней, который делает доступными только из hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a68f-105">hello API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within hello Virtual Network.</span></span> <span data-ttu-id="9a68f-106">Шлюз приложений Azure — это служба PaaS, выполняющая функции подсистемы балансировки нагрузки на сетевом уровне 7.</span><span class="sxs-lookup"><span data-stu-id="9a68f-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="9a68f-107">Это служба обратного прокси-сервера, которая содержит также брандмауэр веб-приложения (WAF).</span><span class="sxs-lookup"><span data-stu-id="9a68f-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="9a68f-108">Объединение API управления подготовкой в внутренней виртуальной сети с сервера переднего плана для шлюза приложения hello обеспечивает hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="9a68f-108">Combining API Management provisioned in an internal VNET with hello Application Gateway frontend enables hello following scenarios:</span></span>

* <span data-ttu-id="9a68f-109">Используйте hello же ресурсов API-Интерфейс управления для использования, потребители внутренних и внешних потребителей.</span><span class="sxs-lookup"><span data-stu-id="9a68f-109">Use hello same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="9a68f-110">Использовать один ресурс управления API, определив для него в службе управления API подмножество API-интерфейсов, доступных для внешних потребителей.</span><span class="sxs-lookup"><span data-stu-id="9a68f-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="9a68f-111">Укажите способ под ключ tooswitch доступа tooAPI управления из hello общедоступный Интернет и отключать.</span><span class="sxs-lookup"><span data-stu-id="9a68f-111">Provide a turn-key way tooswitch access tooAPI Management from hello public Internet on and off.</span></span> 

##<span data-ttu-id="9a68f-112"><a name="scenario"> </a> Сценарий</span><span class="sxs-lookup"><span data-stu-id="9a68f-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="9a68f-113">В этой статье будет охватывать как toouse единого управления API службы для внутренних и внешних потребителей и сделать ее выступать в качестве одного сервера переднего плана для обоих локальных и облачных API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="9a68f-113">This article will cover how toouse a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="9a68f-114">Также отображается как tooexpose только подмножество собственные интерфейсы API (в примере hello, они будут выделены зеленым цветом) для внешнего использования, с помощью hello PathBasedRouting функциональные возможности, доступные в шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="9a68f-114">You will also see how tooexpose only a subset of your APIs (in hello example they are highlighted in green) for External Consumption using hello PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="9a68f-115">В первом примере установки hello все интерфейсы API можно управлять только с внутри виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a68f-115">In hello first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="9a68f-116">Внутренние потребители (выделены оранжевым цветом) могут обращаться ко всем внутренним и внешним API.</span><span class="sxs-lookup"><span data-stu-id="9a68f-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="9a68f-117">Трафик никогда не идет через цепи Express Route tooInternet доставки высокой производительности.</span><span class="sxs-lookup"><span data-stu-id="9a68f-117">Traffic never goes out tooInternet a high performance is delivered via Express Route circuits.</span></span>

![Маршрут URL-адреса](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="9a68f-119"><a name="before-you-begin"> </a> Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9a68f-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="9a68f-120">Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="9a68f-121">Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9a68f-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="9a68f-122">Создайте виртуальную сеть и отдельные подсети в ней для службы управления API и шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="9a68f-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="9a68f-123">Если предполагается toocreate пользовательского DNS-сервера для hello виртуальной сети, сделать это перед началом развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-123">If you intend toocreate a custom DNS server for hello Virtual Network, do so before starting hello deployment.</span></span> <span data-ttu-id="9a68f-124">Проверьте ее работы за счет того, виртуальную машину, созданную в новую подсеть в hello виртуальной сети можно разрешить и открывать все конечные точки службы Azure.</span><span class="sxs-lookup"><span data-stu-id="9a68f-124">Double check it works by ensuring a virtual machine created in a new subnet in hello Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="9a68f-125">Что такое необходимые toocreate интеграцию между API управления и шлюз приложений?</span><span class="sxs-lookup"><span data-stu-id="9a68f-125">What is required toocreate an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="9a68f-126">**Пул серверных:** это hello внутренний виртуальный IP-адрес hello службы управления API.</span><span class="sxs-lookup"><span data-stu-id="9a68f-126">**Back-end server pool:** This is hello internal virtual IP address of hello API Management service.</span></span>
* <span data-ttu-id="9a68f-127">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="9a68f-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="9a68f-128">Эти параметры используются примененных tooall серверы в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-128">These settings are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="9a68f-129">**Интерфейсный порт:** hello открытый порт, открытый для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-129">**Front-end port:** This is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="9a68f-130">Трафик попадание он получает перенаправленный tooone hello внутренними серверами.</span><span class="sxs-lookup"><span data-stu-id="9a68f-130">Traffic hitting it gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="9a68f-131">**Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).</span><span class="sxs-lookup"><span data-stu-id="9a68f-131">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="9a68f-132">**Правило:** правило hello привязывает пул серверных tooa прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="9a68f-132">**Rule:** hello rule binds a listener tooa back-end server pool.</span></span>
* <span data-ttu-id="9a68f-133">**Пользовательский зонд работоспособности:** шлюз приложений по умолчанию использует IP адрес на основе проб toofigure какие серверов в hello BackendAddressPool активны.</span><span class="sxs-lookup"><span data-stu-id="9a68f-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes toofigure out which servers in hello BackendAddressPool are active.</span></span> <span data-ttu-id="9a68f-134">Hello службы управления API отвечает только toorequests, имеющих правильный заголовок hello, поэтому пробы по умолчанию hello сбой.</span><span class="sxs-lookup"><span data-stu-id="9a68f-134">hello API Management service only responds toorequests which have hello correct host header, hence hello default probes fail.</span></span> <span data-ttu-id="9a68f-135">Зонд пользовательских работоспособности требуется toobe определенные toohelp шлюз приложений определить hello служба находится в активном состоянии и пересылать запросы.</span><span class="sxs-lookup"><span data-stu-id="9a68f-135">A custom health probe needs toobe defined toohelp application gateway determine that hello service is alive and it should forward requests.</span></span>
* <span data-ttu-id="9a68f-136">**Сертификат для пользовательского домена:** tooaccess управления API из hello Интернет необходимо toocreate сопоставление CNAME его имя узла toohello шлюз приложений интерфейса DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="9a68f-136">**Custom domain certificate:** tooaccess API Management from hello internet you need toocreate a CNAME mapping of its hostname toohello Application Gateway front-end DNS name.</span></span> <span data-ttu-id="9a68f-137">Это обеспечивает hello заголовок узла и сертификат, отправленный tooApplication шлюза, который пересылается tooAPI управления, который APIM может распознать как допустимый.</span><span class="sxs-lookup"><span data-stu-id="9a68f-137">This ensures that hello hostname header and certificate sent tooApplication Gateway that is forwarded tooAPI Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="9a68f-138"><a name="overview-steps"> </a> Действия по интеграции управления API со шлюзом приложений</span><span class="sxs-lookup"><span data-stu-id="9a68f-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="9a68f-139">Создание группы ресурсов для диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9a68f-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="9a68f-140">Создайте виртуальную сеть, подсеть и общедоступный IP-адрес для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-140">Create a Virtual Network, subnet, and public IP for hello Application Gateway.</span></span> <span data-ttu-id="9a68f-141">Создайте еще одну подсеть для управления API.</span><span class="sxs-lookup"><span data-stu-id="9a68f-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="9a68f-142">Создать службу управления API внутри hello подсети виртуальной сети, созданной ранее и убедитесь, что используется внутренний режим hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-142">Create an API Management service inside hello VNET subnet created above and ensure you use hello Internal mode.</span></span>
4. <span data-ttu-id="9a68f-143">Настройте пользовательское доменное имя hello в службе управления API hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-143">Setup hello custom domain name in hello API Management service.</span></span>
5. <span data-ttu-id="9a68f-144">Создайте объект конфигурации шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="9a68f-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="9a68f-145">Создайте ресурс шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="9a68f-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="9a68f-146">Создайте запись CNAME из hello открытому DNS-имени имя узла прокси-сервера управления API toohello шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-146">Create a CNAME from hello public DNS name of hello Application Gateway toohello API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="9a68f-147">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="9a68f-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="9a68f-148">Убедитесь, что используется последняя версия Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-148">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="9a68f-149">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9a68f-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="9a68f-150">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="9a68f-150">Step 1</span></span>

<span data-ttu-id="9a68f-151">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="9a68f-151">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="9a68f-152">Выполните аутентификацию со своими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="9a68f-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="9a68f-153">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="9a68f-153">Step 2</span></span>

<span data-ttu-id="9a68f-154">Проверьте hello подписки для учетной записи hello и выберите его.</span><span class="sxs-lookup"><span data-stu-id="9a68f-154">Check hello subscriptions for hello account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="9a68f-155">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="9a68f-155">Step 3</span></span>

<span data-ttu-id="9a68f-156">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="9a68f-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="9a68f-157">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="9a68f-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="9a68f-158">Используется как расположение по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9a68f-158">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="9a68f-159">Убедитесь, что все команды toocreate hello использование шлюза приложений одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9a68f-159">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="9a68f-160">Создание виртуальной сети и подсети для шлюза приложения hello</span><span class="sxs-lookup"><span data-stu-id="9a68f-160">Create a Virtual Network and a subnet for hello application gateway</span></span>

<span data-ttu-id="9a68f-161">Hello в следующем примере показано, как toocreate виртуальной сети с помощью hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9a68f-161">hello following example shows how toocreate a Virtual Network using hello resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="9a68f-162">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="9a68f-162">Step 1</span></span>

<span data-ttu-id="9a68f-163">Назначьте hello адрес диапазона 10.0.0.0/24 toohello подсети переменной toobe использовать для шлюза приложения при создании виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a68f-163">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="9a68f-164">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="9a68f-164">Step 2</span></span>

<span data-ttu-id="9a68f-165">Назначьте hello адрес диапазона 10.0.1.0/24 toohello подсети переменной toobe используется для управления API при создании виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a68f-165">Assign hello address range 10.0.1.0/24 toohello subnet variable toobe used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="9a68f-166">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="9a68f-166">Step 3</span></span>

<span data-ttu-id="9a68f-167">Создайте виртуальную сеть с именем **appgwvnet** в группе ресурсов **apim appGw группы Маршрутизации** для регионе hello Запад США, с помощью 10.0.0.0/16 hello префикс подсети 10.0.0.0/24 и 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="9a68f-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for hello West US region using hello prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="9a68f-168">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="9a68f-168">Step 4</span></span>

<span data-ttu-id="9a68f-169">Присвоить значение переменной подсети для получения дальнейших указаний hello</span><span class="sxs-lookup"><span data-stu-id="9a68f-169">Assign a subnet variable for hello next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="9a68f-170">Создание службы управления API в виртуальной сети, настроенной в режиме внутренней сети</span><span class="sxs-lookup"><span data-stu-id="9a68f-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="9a68f-171">Hello следующем примере показано, как toocreate службу управления API в виртуальной сети настроена только для внутренней.</span><span class="sxs-lookup"><span data-stu-id="9a68f-171">hello following example shows how toocreate an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="9a68f-172">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="9a68f-172">Step 1</span></span>
<span data-ttu-id="9a68f-173">Создайте объект API управления виртуальной сети с помощью подсети hello $apimsubnetdata созданной выше.</span><span class="sxs-lookup"><span data-stu-id="9a68f-173">Create an API Management Virtual Network object using hello subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="9a68f-174">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="9a68f-174">Step 2</span></span>
<span data-ttu-id="9a68f-175">Создание службы управления API внутри hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a68f-175">Create an API Management service inside hello Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="9a68f-176">После успешного завершения hello выше команда ссылаться слишком[tooaccess внутреннюю службу управления API виртуальной сети требуется настройки DNS](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess его.</span><span class="sxs-lookup"><span data-stu-id="9a68f-176">After hello above command succeeds refer too[DNS Configuration required tooaccess internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="9a68f-177">Настройка пользовательского доменного имени в службе управления API</span><span class="sxs-lookup"><span data-stu-id="9a68f-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="9a68f-178">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="9a68f-178">Step 1</span></span>
<span data-ttu-id="9a68f-179">Отправьте hello сертификат с закрытым ключом для домена hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-179">Upload hello certificate with private key for hello domain.</span></span> <span data-ttu-id="9a68f-180">В нашем примере это `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="9a68f-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="9a68f-181">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="9a68f-181">Step 2</span></span>
<span data-ttu-id="9a68f-182">После отправки сертификата hello создать объект конфигурации имя узла для hello прокси-сервера с именем узла из `api.contoso.net`, как сертификат пример hello обеспечивает полномочия для hello `*.contoso.net` домена.</span><span class="sxs-lookup"><span data-stu-id="9a68f-182">Once hello certificate is uploaded, create a hostname configuration object for hello proxy with a hostname of `api.contoso.net`, as hello example certificate provides authority for hello  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="9a68f-183">Создать общедоступный IP-адрес для интерфейса конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="9a68f-183">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="9a68f-184">Создание общих ресурсов IP **publicIP01** в группе ресурсов **apim appGw-RG** для региона hello Запад США.</span><span class="sxs-lookup"><span data-stu-id="9a68f-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="9a68f-185">IP-адрес назначается шлюз приложений toohello при запуске службы hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-185">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="9a68f-186">Создание конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="9a68f-186">Create application gateway configuration</span></span>

<span data-ttu-id="9a68f-187">Необходимо настроить все элементы конфигурации, перед созданием шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-187">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="9a68f-188">Hello следующие действия создадут hello элементы конфигурации, которые необходимы для ресурса шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="9a68f-188">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="9a68f-189">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="9a68f-189">Step 1</span></span>

<span data-ttu-id="9a68f-190">Создайте конфигурацию IP-адресов шлюза приложений с именем **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="9a68f-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="9a68f-191">При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и маршрутизацию сетевого трафика toohello IP-адресов в пул IP-адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-191">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="9a68f-192">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="9a68f-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="9a68f-193">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="9a68f-193">Step 2</span></span>

<span data-ttu-id="9a68f-194">Настройте hello интерфейсный IP-порт для hello общедоступную конечную точку IP.</span><span class="sxs-lookup"><span data-stu-id="9a68f-194">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="9a68f-195">Это используется порт hello, конечные пользователи подключены.</span><span class="sxs-lookup"><span data-stu-id="9a68f-195">This port is hello port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="9a68f-196">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="9a68f-196">Step 3</span></span>

<span data-ttu-id="9a68f-197">Настройте интерфейсный IP hello общедоступную конечную точку IP.</span><span class="sxs-lookup"><span data-stu-id="9a68f-197">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="9a68f-198">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="9a68f-198">Step 4</span></span>

<span data-ttu-id="9a68f-199">Настройте сертификат hello для hello шлюз приложений, используемых toodecrypt и повторное шифрование трафика hello, проходящие через.</span><span class="sxs-lookup"><span data-stu-id="9a68f-199">Configure hello certificate for hello Application Gateway, used toodecrypt and re-encrypt hello traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="9a68f-200">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="9a68f-200">Step 5</span></span>

<span data-ttu-id="9a68f-201">Создайте прослушиватель HTTP hello для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-201">Create hello HTTP listener for hello Application Gateway.</span></span> <span data-ttu-id="9a68f-202">Назначьте hello интерфейсный IP-конфигурации, порта и tooit сертификат ssl.</span><span class="sxs-lookup"><span data-stu-id="9a68f-202">Assign hello front-end IP configuration, port, and ssl certificate tooit.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="9a68f-203">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="9a68f-203">Step 6</span></span>

<span data-ttu-id="9a68f-204">Создать пользовательский зонд toohello службы управления API `ContosoApi` конечная точка прокси для домена.</span><span class="sxs-lookup"><span data-stu-id="9a68f-204">Create a custom probe toohello API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="9a68f-205">путь Hello `/status-0123456789abcdef` работоспособности конечной точки по умолчанию, размещенных на все службы управления API hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-205">hello path `/status-0123456789abcdef` is a default health endpoint hosted on all hello API Management services.</span></span> <span data-ttu-id="9a68f-206">Задать `api.contoso.net` как toosecure пользовательский зонд имя узла с помощью SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="9a68f-206">Set `api.contoso.net` as a custom probe hostname toosecure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="9a68f-207">Здравствуйте, имя узла `contosoapi.azure-api.net` узла прокси-сервера по умолчанию hello настраивается при службы с именем `contosoapi` создается в открытый Azure.</span><span class="sxs-lookup"><span data-stu-id="9a68f-207">hello hostname `contosoapi.azure-api.net` is hello default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="9a68f-208">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="9a68f-208">Step 7</span></span>

<span data-ttu-id="9a68f-209">Отправьте сертификат hello toobe используется hello протокол SSL включен внутреннего пула ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9a68f-209">Upload hello certificate toobe used on hello SSL-enabled backend pool resources.</span></span> <span data-ttu-id="9a68f-210">Это hello же сертификат, который вы указали в шаге 4 выше.</span><span class="sxs-lookup"><span data-stu-id="9a68f-210">This is hello same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a><span data-ttu-id="9a68f-211">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="9a68f-211">Step 8</span></span>

<span data-ttu-id="9a68f-212">Серверная часть настройки для hello шлюз приложений HTTP.</span><span class="sxs-lookup"><span data-stu-id="9a68f-212">Configure HTTP backend settings for hello Application Gateway.</span></span> <span data-ttu-id="9a68f-213">К настройкам относится и предел времени ожидания, по истечении которого запрос к внутренним серверам отменяется.</span><span class="sxs-lookup"><span data-stu-id="9a68f-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="9a68f-214">Это значение отличается от времени ожидания проверки hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-214">This value is different from hello probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="9a68f-215">Шаг 9.</span><span class="sxs-lookup"><span data-stu-id="9a68f-215">Step 9</span></span>

<span data-ttu-id="9a68f-216">Настройка внутренней пул IP-адресов с именем **apimbackend** hello внутренний виртуальный IP-адрес службы управления API hello созданной выше.</span><span class="sxs-lookup"><span data-stu-id="9a68f-216">Configure a back-end IP address pool named **apimbackend**  with hello internal virtual IP address of hello API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="9a68f-217">Шаг 10</span><span class="sxs-lookup"><span data-stu-id="9a68f-217">Step 10</span></span>

<span data-ttu-id="9a68f-218">Создайте параметры для фиктивного (несуществующего) внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="9a68f-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="9a68f-219">Пути tooAPI запросы, которые нам не нужно будет попаданий этой базы данных и возвращают 404 tooexpose из API управления через шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="9a68f-219">Requests tooAPI paths that we do not want tooexpose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="9a68f-220">Настройте параметры HTTP для внутреннего фиктивный hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-220">Configure HTTP settings for hello dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="9a68f-221">Настройка фиктивный серверной **dummyBackendPool**, который указывает адрес полного доменного ИМЕНИ tooa **dummybackend.com**. Этот адрес полного доменного ИМЕНИ не существует в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-221">Configure a dummy backend **dummyBackendPool**, which points tooa FQDN address **dummybackend.com**. This FQDN address does not exist in hello virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="9a68f-222">Создать правило, установка этого hello, будет использовать шлюз приложения по умолчанию, указывающая серверной несуществующий toohello **dummybackend.com** в hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a68f-222">Create a rule setting that hello Application Gateway will use by default which points toohello non-existent backend **dummybackend.com** in hello Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="9a68f-223">Шаг 11</span><span class="sxs-lookup"><span data-stu-id="9a68f-223">Step 11</span></span>

<span data-ttu-id="9a68f-224">Настройте правило пути URL-адресов для пулов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="9a68f-224">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="9a68f-225">Это позволяет, выбор только некоторые hello интерфейсы API управления API, предоставляемые toohello public.</span><span class="sxs-lookup"><span data-stu-id="9a68f-225">This enables selecting only some of hello APIs from API Management for being exposed toohello public.</span></span> <span data-ttu-id="9a68f-226">Например, из набора `Echo API` (/echo/), `Calculator API` (/calc/) и т. д. сделать доступным из Интернета только `Echo API`.</span><span class="sxs-lookup"><span data-stu-id="9a68f-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="9a68f-227">Hello пример создает простое правило для hello «/ echo /» путь маршрутизации трафика toohello серверной части «apimProxyBackendPool».</span><span class="sxs-lookup"><span data-stu-id="9a68f-227">hello following example creates a simple rule for hello "/echo/" path routing traffic toohello back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="9a68f-228">Если путь hello не соответствует пути hello правила мы хотим tooenable из системы управления API, путь конфигурации карты также настраивает пула адресов серверной части по умолчанию с именем правила hello **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="9a68f-228">If hello path doesn't match hello path rules we want tooenable from API Management, hello rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="9a68f-229">Например, http://api.contoso.net/calc/ * становится слишком**dummyBackendPool** как она определена в качестве пула по умолчанию hello несовпадающие трафика.</span><span class="sxs-lookup"><span data-stu-id="9a68f-229">For example, http://api.contoso.net/calc/* goes too**dummyBackendPool** as it is defined as hello default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="9a68f-230">Hello выше шаг гарантирует только по запросу для hello путь «/ echo» разрешается доступ через шлюз приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-230">hello above step ensures that only requests for hello path "/echo" are allowed through hello Application Gateway.</span></span> <span data-ttu-id="9a68f-231">Запросы tooother настроенного API-интерфейсов в API управления вызовет ошибки 404 из шлюза приложения, если доступ осуществляется из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-231">Requests tooother APIs configured in API Management will throw 404 errors from Application Gateway when accessed from hello Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="9a68f-232">Шаг 12</span><span class="sxs-lookup"><span data-stu-id="9a68f-232">Step 12</span></span>

<span data-ttu-id="9a68f-233">Создание параметра правила для hello шлюз приложений toouse URL-адрес на основе пути маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="9a68f-233">Create a rule setting for hello Application Gateway toouse URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="9a68f-234">Шаг 13</span><span class="sxs-lookup"><span data-stu-id="9a68f-234">Step 13</span></span>

<span data-ttu-id="9a68f-235">Настройте hello число экземпляров и размер для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-235">Configure hello number of instances and size for hello Application Gateway.</span></span> <span data-ttu-id="9a68f-236">Здесь мы используем hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) для повышения уровня безопасности hello ресурса управления API.</span><span class="sxs-lookup"><span data-stu-id="9a68f-236">Here we are using hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of hello API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="9a68f-237">Шаг 14</span><span class="sxs-lookup"><span data-stu-id="9a68f-237">Step 14</span></span>

<span data-ttu-id="9a68f-238">Настройка WAF toobe в режиме «Защита».</span><span class="sxs-lookup"><span data-stu-id="9a68f-238">Configure WAF toobe in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="9a68f-239">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="9a68f-239">Create Application Gateway</span></span>

<span data-ttu-id="9a68f-240">Создание шлюза приложения со всеми объектами конфигурации hello из hello в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="9a68f-240">Create an Application Gateway with all hello configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a><span data-ttu-id="9a68f-241">Запись CNAME hello API управления прокси-сервера имя узла toohello открытому DNS-имени hello ресурсов шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="9a68f-241">CNAME hello API Management proxy hostname toohello public DNS name of hello Application Gateway resource</span></span>

<span data-ttu-id="9a68f-242">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="9a68f-242">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="9a68f-243">При использовании общедоступных IP-адресов, шлюз приложений требуется динамически назначаемый имени DNS, которое может быть легко toouse.</span><span class="sxs-lookup"><span data-stu-id="9a68f-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy toouse.</span></span> 

<span data-ttu-id="9a68f-244">Hello шлюз приложений DNS-имя должно быть используется toocreate запись CNAME, которое указывает имя узла hello APIM прокси-сервера (например `api.contoso.net` в вышеприведенных примерах hello) toothis DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="9a68f-244">hello Application Gateway's DNS name should be used toocreate a CNAME record which points hello APIM proxy host name (e.g. `api.contoso.net` in hello examples above) toothis DNS name.</span></span> <span data-ttu-id="9a68f-245">tooconfigure hello интерфейсных IP запись CNAME, получить hello сведения о hello шлюз приложений и соответствующее IP или DNS-имя с помощью элемента PublicIPAddress hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-245">tooconfigure hello frontend IP CNAME record, retrieve hello details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element.</span></span> <span data-ttu-id="9a68f-246">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезапуске шлюза.</span><span class="sxs-lookup"><span data-stu-id="9a68f-246">hello use of A-records is not recommended since hello VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="9a68f-247"><a name="summary"> </a> Сводка</span><span class="sxs-lookup"><span data-stu-id="9a68f-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="9a68f-248">Управления API Azure, настроенные в виртуальной сети предоставляет интерфейс один шлюз для всех настроенных интерфейсов API, размещенной в локальной среде ли они в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="9a68f-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in hello cloud.</span></span> <span data-ttu-id="9a68f-249">Интеграция шлюза приложений со службой управления API обеспечивает гибкость hello выборочного включения определенного toobe API-интерфейсы доступны на hello Интернета, а также предоставление брандмауэр веб-приложения как экземпляр интерфейса API управления tooyour переднего плана.</span><span class="sxs-lookup"><span data-stu-id="9a68f-249">Integrating Application Gateway with API Management provides hello flexibility of selectively enabling particular APIs toobe accessible on hello Internet, as well as providing a Web Application Firewall as a frontend tooyour API Management instance.</span></span>

##<span data-ttu-id="9a68f-250"><a name="next-steps"> </a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a68f-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="9a68f-251">Дополнительные сведения о шлюзе приложений Azure:</span><span class="sxs-lookup"><span data-stu-id="9a68f-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="9a68f-252">Обзор шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="9a68f-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * <span data-ttu-id="9a68f-253">[Application Gateway Web Application Firewall (preview)](../application-gateway/application-gateway-webapplicationfirewall-overview.md) (Брандмауэр веб-приложения шлюза приложений (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="9a68f-253">[Application Gateway Web Application Firewall](../application-gateway/application-gateway-webapplicationfirewall-overview.md)</span></span>
  * [<span data-ttu-id="9a68f-254">Создание шлюза приложений с помощью маршрутизации на основе пути</span><span class="sxs-lookup"><span data-stu-id="9a68f-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="9a68f-255">См. дополнительные сведения о службе управлении API и виртуальных сетях</span><span class="sxs-lookup"><span data-stu-id="9a68f-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="9a68f-256">С помощью API управления доступен только в пределах hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="9a68f-256">Using API Management available only within hello VNET</span></span>](api-management-using-with-internal-vnet.md)
  * <span data-ttu-id="9a68f-257">[How to use Azure API Management with virtual networks](api-management-using-with-vnet.md) (Использование управления API Azure в виртуальных сетях)</span><span class="sxs-lookup"><span data-stu-id="9a68f-257">[Using API Management in VNET](api-management-using-with-vnet.md)</span></span>
