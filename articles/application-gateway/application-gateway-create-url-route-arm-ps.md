---
title: "правила с помощью маршрутизации URL-адрес шлюза приложения aaaCreate | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, настройте шлюз приложения Azure с помощью правила маршрутизации URL-адрес"
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
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="20a95-103">Создание шлюза приложений с помощью маршрутизации на основе пути</span><span class="sxs-lookup"><span data-stu-id="20a95-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="20a95-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="20a95-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="20a95-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="20a95-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="20a95-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="20a95-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="20a95-107">Маршрутизация URL-адрес на основе пути позволяет вам tooassociate маршрутов на основе hello пути URL-адреса HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="20a95-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="20a95-108">Он проверяет, существует ли пул серверной части tooa маршрута, настроенный для hello URL-адрес, представленных в hello шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="20a95-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway.</span></span> <span data-ttu-id="20a95-109">После этого он отправляет hello сетевой трафик toohello определенного пула серверной части.</span><span class="sxs-lookup"><span data-stu-id="20a95-109">It then sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="20a95-110">Обычно используются для маршрутизации на основе URL-адрес — tooload балансировать нагрузку по запросам для различных типов содержимого toodifferent серверных пулов.</span><span class="sxs-lookup"><span data-stu-id="20a95-110">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="20a95-111">Маршрутизация на основе URL-адрес появился новый шлюз tooapplication тип правила.</span><span class="sxs-lookup"><span data-stu-id="20a95-111">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="20a95-112">Шлюз приложений имеет два типа правил: базовые правила и правила на основе пути.</span><span class="sxs-lookup"><span data-stu-id="20a95-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="20a95-113">Основное правило тип предоставляет циклического службы для внутреннего интерфейса hello пулов при PathBasedRouting Кроме распространения tooround циклический перебор, также учитывает шаблон пути URL-адреса запроса hello при выборе hello внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="20a95-113">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="20a95-114">Сценарий</span><span class="sxs-lookup"><span data-stu-id="20a95-114">Scenario</span></span>

<span data-ttu-id="20a95-115">В следующем примере hello, шлюз приложений обслуживает трафика для contoso.com с помощью двух серверных пулов: видео сервера пул и пул серверов изображения.</span><span class="sxs-lookup"><span data-stu-id="20a95-115">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="20a95-116">Запросы на http://contoso.com/image * направляются в пул серверов tooimage (pool1) и http://contoso.com/video * направляются пул серверов toovideo (pool2).</span><span class="sxs-lookup"><span data-stu-id="20a95-116">Requests for http://contoso.com/image* are routed tooimage server pool (pool1), and http://contoso.com/video* are routed toovideo server pool (pool2).</span></span> <span data-ttu-id="20a95-117">Если ни один из шаблонов путей hello соответствует выбирается пула сервера по умолчанию (pool1).</span><span class="sxs-lookup"><span data-stu-id="20a95-117">if none of hello path patterns match, a default server pool (pool1) is selected.</span></span>

![Маршрут URL-адреса](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="20a95-119">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="20a95-119">Before you begin</span></span>

1. <span data-ttu-id="20a95-120">Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="20a95-121">Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="20a95-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="20a95-122">Создайте виртуальную сеть и подсеть для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="20a95-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="20a95-123">Убедитесь, что нет виртуальных машин или развертывания в облаке hello подсети.</span><span class="sxs-lookup"><span data-stu-id="20a95-123">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="20a95-124">шлюз приложения Hello должен быть сам по себе в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="20a95-124">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="20a95-125">серверы Hello добавлены серверной части пула toouse toohello hello использование шлюза приложений должен существовать или в виртуальной сети hello или открытый IP/VIP-адрес, назначенный созданы их конечные точки.</span><span class="sxs-lookup"><span data-stu-id="20a95-125">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="20a95-126">Что такое необходимые toocreate шлюза приложения</span><span class="sxs-lookup"><span data-stu-id="20a95-126">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="20a95-127">**Пул серверных:** hello список IP-адресов серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="20a95-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="20a95-128">Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="20a95-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="20a95-129">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="20a95-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="20a95-130">Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="20a95-131">**Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="20a95-132">Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="20a95-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="20a95-133">**Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).</span><span class="sxs-lookup"><span data-stu-id="20a95-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="20a95-134">**Правило:** правило hello привязывает hello прослушивателя, пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="20a95-134">**Rule:** hello rule binds hello listener, hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="20a95-135">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="20a95-135">Create an application gateway</span></span>

<span data-ttu-id="20a95-136">Hello различие между использованием классический Azure и Azure Resource Manager — создать шлюз приложения hello и hello элементы, которые должны toobe настроить порядок hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-136">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="20a95-137">С помощью диспетчера ресурсов все элементы, которые делают шлюза приложения настраиваются отдельно, а затем указать ресурс шлюза приложения hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="20a95-137">With Resource Manager, all items that make an application gateway are configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="20a95-138">Ниже приведены шаги hello, необходимые toocreate шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="20a95-138">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="20a95-139">Создание группы ресурсов для диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="20a95-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="20a95-140">Создайте виртуальную сеть, подсеть и общедоступный IP-адрес для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-140">Create a virtual network, subnet, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="20a95-141">Создание объекта конфигурации шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="20a95-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="20a95-142">Создание ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="20a95-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="20a95-143">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="20a95-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="20a95-144">Убедитесь, что используется последняя версия Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-144">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="20a95-145">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="20a95-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="20a95-146">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="20a95-146">Step 1</span></span>

<span data-ttu-id="20a95-147">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="20a95-147">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="20a95-148">С помощью учетных данных, запрашиваемых tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="20a95-148">You are prompted tooauthenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="20a95-149">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="20a95-149">Step 2</span></span>

<span data-ttu-id="20a95-150">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-150">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="20a95-151">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="20a95-151">Step 3</span></span>

<span data-ttu-id="20a95-152">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="20a95-152">Choose which of your Azure subscriptions toouse.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="20a95-153">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="20a95-153">Step 4</span></span>

<span data-ttu-id="20a95-154">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="20a95-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="20a95-155">В качестве альтернативы можно также создать теги группы ресурсов для шлюза приложений:</span><span class="sxs-lookup"><span data-stu-id="20a95-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="20a95-156">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="20a95-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="20a95-157">Эта группа ресурсов используются как расположение по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="20a95-157">This resource group is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="20a95-158">Убедитесь, что все команды toocreate hello использование шлюза приложений одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="20a95-158">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="20a95-159">В приведенном выше примере hello мы создали группу ресурсов под названием «appgw RG» и расположение «West US».</span><span class="sxs-lookup"><span data-stu-id="20a95-159">In hello example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="20a95-160">Если вам требуется пользовательский зонд tooconfigure шлюза приложения, см. раздел [создать шлюз приложений с пользовательской проверки с помощью PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="20a95-160">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="20a95-161">Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20a95-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="20a95-162">Создание виртуальной сети и подсети для шлюза приложения hello</span><span class="sxs-lookup"><span data-stu-id="20a95-162">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="20a95-163">Следующий пример показывает как Hello toocreate виртуальной сети с помощью диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="20a95-163">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="20a95-164">В этом примере создается виртуальная сеть для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-164">This example creates a VNET for hello Application Gateway.</span></span> <span data-ttu-id="20a95-165">Шлюз приложений требуется собственный подсети по этой причине hello подсети для шлюза приложения hello меньше, чем hello адресное пространство виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="20a95-165">Application Gateway requires its own subnet, for this reason hello subnet created for hello Application Gateway is smaller than hello VNET address space.</span></span> <span data-ttu-id="20a95-166">Это обеспечивает другие ресурсы, включая, но не только tooweb toobe серверы настроить в hello же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="20a95-166">This allows for other resources, including but not limited tooweb servers toobe configured in hello same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="20a95-167">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="20a95-167">Step 1</span></span>

<span data-ttu-id="20a95-168">Назначьте hello диапазон адресов 10.0.0.0/24 toohello подсети переменной toobe используется toocreate виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="20a95-168">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toocreate a virtual network.</span></span>  <span data-ttu-id="20a95-169">Это создает hello объекта конфигурации подсети для шлюза приложения, который используется в следующем примере hello hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-169">This creates hello subnet configuration object for hello Application Gateway, which is used in hello next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="20a95-170">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="20a95-170">Step 2</span></span>

<span data-ttu-id="20a95-171">Создайте виртуальную сеть с именем **appgwvnet** в группе ресурсов **appgw rg** для региона hello Запад США, с 10.0.0.0/16 hello префикс подсети 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="20a95-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="20a95-172">Это завершает конфигурацию hello hello виртуальную сеть с одной подсетью для hello tooreside шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="20a95-172">This completes hello configuration of hello VNET with a single subnet for hello Application Gateway tooreside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="20a95-173">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="20a95-173">Step 3</span></span>

<span data-ttu-id="20a95-174">Присвойте переменной hello подсети для hello дальнейшие действия, он передается toohello `New-AzureRMApplicationGateway` командлета на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="20a95-174">Assign hello subnet variable for hello next steps, this is passed toohello `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="20a95-175">Создать общедоступный IP-адрес для интерфейса конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="20a95-175">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="20a95-176">Создание общих ресурсов IP **publicIP01** в группе ресурсов **appgw rg** для региона hello Запад США.</span><span class="sxs-lookup"><span data-stu-id="20a95-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="20a95-177">Шлюз приложений можно использовать общедоступный IP-адрес, внутренний IP-адрес или обоих запросов tooreceive для балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="20a95-177">Application Gateway can use a public IP address, internal IP address or both tooreceive requests for load balancing.</span></span>  <span data-ttu-id="20a95-178">В этом примере используется общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="20a95-178">This example only uses a public IP address.</span></span> <span data-ttu-id="20a95-179">В следующем примере hello имя DNS не настраивается для создания hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="20a95-179">In hello following example, no DNS name is configured for creating hello Public IP address.</span></span>  <span data-ttu-id="20a95-180">Шлюз приложений не поддерживает пользовательские DNS-имена в общедоступных IP-адресах.</span><span class="sxs-lookup"><span data-stu-id="20a95-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="20a95-181">Если пользовательское имя является обязательным для hello общедоступную конечную точку, запись CNAME должны создаваться toopoint toohello автоматически создается DNS-имя для hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="20a95-181">If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="20a95-182">IP-адрес назначается шлюз приложений toohello при запуске службы hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-182">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="20a95-183">Создание конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="20a95-183">Create application gateway configuration</span></span>

<span data-ttu-id="20a95-184">Необходимо настроить все элементы конфигурации, перед созданием шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-184">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="20a95-185">Hello следующие действия создадут hello элементы конфигурации, которые необходимы для ресурса шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="20a95-185">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="20a95-186">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="20a95-186">Step 1</span></span>

<span data-ttu-id="20a95-187">Создайте конфигурацию IP-адресов шлюза приложений с именем **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="20a95-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="20a95-188">При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и маршрутизацию сетевого трафика toohello IP-адресов в пул IP-адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-188">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="20a95-189">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="20a95-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="20a95-190">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="20a95-190">Step 2</span></span>

<span data-ttu-id="20a95-191">Настройка hello серверной части IP-адресов с именем **pool01** и **pool2** с IP-адреса для **pool1** и **pool2**.</span><span class="sxs-lookup"><span data-stu-id="20a95-191">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="20a95-192">Эти IP-адреса — hello IP-адреса ресурсов hello, размещающие приложения hello web toobe с защищен шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-192">These IP addresses are hello IP addresses of hello resources that are hosting hello web application toobe protected by hello application gateway.</span></span> <span data-ttu-id="20a95-193">Эти члены пула серверной части являются все проверенные toobe зонды работоспособности как основные проверки, так и пользовательские зонды.</span><span class="sxs-lookup"><span data-stu-id="20a95-193">These backend pool members are all validated toobe healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="20a95-194">Трафик направляется toothem при поступлении запросов на шлюз приложения hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-194">Traffic is then routed toothem when requests come into hello application gateway.</span></span> <span data-ttu-id="20a95-195">Внутренние пулы может использоваться несколько правил в шлюза приложения hello, что означает один внутренний пул может использоваться для нескольких веб-приложений, которые располагаются на hello таким же узла.</span><span class="sxs-lookup"><span data-stu-id="20a95-195">Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="20a95-196">В этом примере существует два внутренней пулы tooroute трафика на основе hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="20a95-196">In this example, there are two back-end pools tooroute network traffic based on hello URL path.</span></span> <span data-ttu-id="20a95-197">Один пул принимает трафик для URL-пути /video, а другой — для пути /image.</span><span class="sxs-lookup"><span data-stu-id="20a95-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="20a95-198">Замените hello, предшествующий IP адресов tooadd собственных конечных точек приложения IP адрес.</span><span class="sxs-lookup"><span data-stu-id="20a95-198">Replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="20a95-199">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="20a95-199">Step 3</span></span>

<span data-ttu-id="20a95-200">Настройка параметров шлюза приложения **poolsetting01** и **poolsetting02** hello балансировки нагрузки сетевого трафика в пуле hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="20a95-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="20a95-201">В этом примере вы настройки другой пул серверной части для пулов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="20a95-201">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="20a95-202">Для каждого пула тыловых серверов параметры можно настроить отдельно.</span><span class="sxs-lookup"><span data-stu-id="20a95-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="20a95-203">Параметры HTTP серверной используются членами правила tooroute трафика toohello правильный внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="20a95-203">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="20a95-204">Определяет hello протокол и порт, используемый при отправке трафика члены пула toohello серверной части.</span><span class="sxs-lookup"><span data-stu-id="20a95-204">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="20a95-205">Сеансы на основе файлов cookie, также определяются hello параметров серверного HTTP.</span><span class="sxs-lookup"><span data-stu-id="20a95-205">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="20a95-206">Если параметр включен, сходство сеансов на основе файлов cookie отправляет трафик toohello один внутренний как предыдущие запросы для каждого пакета.</span><span class="sxs-lookup"><span data-stu-id="20a95-206">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="20a95-207">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="20a95-207">Step 4</span></span>

<span data-ttu-id="20a95-208">Настройте интерфейсный IP hello общедоступную конечную точку IP.</span><span class="sxs-lookup"><span data-stu-id="20a95-208">Configure hello front-end IP with public IP endpoint.</span></span> <span data-ttu-id="20a95-209">Hello интерфейсный IP конфигурации используется объект hello toorelate прослушивателя наружу с выходом IP-адрес с hello прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="20a95-209">hello front-end IP configuration object is used by a listener toorelate hello outward facing IP address with hello listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="20a95-210">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="20a95-210">Step 5</span></span>

<span data-ttu-id="20a95-211">Настройте hello интерфейсный порт для шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="20a95-211">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="20a95-212">Объект конфигурации Hello интерфейсный порт используется toodefine прослушивателя что порт прослушивает трафик через прослушиватель hello шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-212">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="20a95-213">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="20a95-213">Step 6</span></span>

<span data-ttu-id="20a95-214">Настройте прослушиватель hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-214">Configure hello listener.</span></span> <span data-ttu-id="20a95-215">Этот шаг позволяет настроить прослушиватель hello hello общедоступный IP-адрес и порт, используемый tooreceive входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="20a95-215">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="20a95-216">Следующий пример Hello принимает hello ранее настроен интерфейсный IP-конфигурации, конфигурацию интерфейсный порт и протокол (http или https) и настраивает hello прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="20a95-216">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="20a95-217">В этом примере hello прослушиватель tooHTTP трафик через порт 80 на hello общедоступный IP-адрес, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="20a95-217">In this example, hello listener listens tooHTTP traffic on port 80 on hello public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="20a95-218">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="20a95-218">Step 7</span></span>

<span data-ttu-id="20a95-219">Настройте правило пути URL-адресов для пулов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="20a95-219">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="20a95-220">Этот шаг настраивает hello относительный путь, используемый шлюзом приложения и определяет сопоставление hello hello URL-адрес и hello внутренней пул, назначенный toohandle hello входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="20a95-220">This step configures hello relative path used by application gateway and defines hello mapping between hello URL path and hello back-end pool that is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20a95-221">Каждый путь должен начинаться с / и hello единственное место «\*» допускается, находится в конце hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-221">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="20a95-222">Примеры допустимых значений: /xyz, /xyz* или /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="20a95-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="20a95-223">Hello строка переданы сопоставителе toohello путь не содержит текст после hello сначала «?» или «#» и эти знаки не допускаются.</span><span class="sxs-lookup"><span data-stu-id="20a95-223">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="20a95-224">Hello в примере создаются два правила: одно для маршрутизации путь «/ изображения /» трафик tooback-end «pool1» и еще один — для маршрутизации трафика tooback-end «pool2.» путь «/ видео и»</span><span class="sxs-lookup"><span data-stu-id="20a95-224">hello following example creates two rules: one for "/image/" path routing traffic tooback-end "pool1" and another one for "/video/" path routing traffic tooback-end "pool2."</span></span> <span data-ttu-id="20a95-225">Эти правила убедитесь, что трафик для каждого набора URL-адресов серверной части перенаправленного toohello.</span><span class="sxs-lookup"><span data-stu-id="20a95-225">These rules ensure that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="20a95-226">Например http://contoso.com/image/figure1.jpg переходит toopool1 и http://contoso.com/video/example.mp4 становится toopool2.</span><span class="sxs-lookup"><span data-stu-id="20a95-226">For example, http://contoso.com/image/figure1.jpg goes toopool1 and http://contoso.com/video/example.mp4 goes toopool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="20a95-227">Если путь hello не соответствует ни одному из правил предопределенный путь hello, hello правило пути карты конфигурация также настраивает пул адресов серверной части по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="20a95-227">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="20a95-228">Например http://contoso.com/shoppingcart/test.html переходит toopool1 как она определена в качестве пула по умолчанию hello для несопоставленных трафика.</span><span class="sxs-lookup"><span data-stu-id="20a95-228">For example, http://contoso.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="20a95-229">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="20a95-229">Step 8</span></span>

<span data-ttu-id="20a95-230">Создайте параметр правила.</span><span class="sxs-lookup"><span data-stu-id="20a95-230">Create a rule setting.</span></span> <span data-ttu-id="20a95-231">Этот шаг позволяет настроить hello приложения шлюза toouse маршрутизация URL-адресов на основе пути.</span><span class="sxs-lookup"><span data-stu-id="20a95-231">This step configures hello application gateway toouse URL path-based routing.</span></span> <span data-ttu-id="20a95-232">Hello `$urlPathMap` переменная, определенная в hello ранее является сейчас используется toocreate hello правила на основе пути.</span><span class="sxs-lookup"><span data-stu-id="20a95-232">hello `$urlPathMap` variable defined in hello earlier step is now used toocreate hello path-based rule.</span></span> <span data-ttu-id="20a95-233">На этом шаге мы связать правило hello прослушивателя и сопоставление пути URL-адрес hello, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="20a95-233">In this step, we associate hello rule with a listener and hello url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="20a95-234">Шаг 9.</span><span class="sxs-lookup"><span data-stu-id="20a95-234">Step 9</span></span>

<span data-ttu-id="20a95-235">Настройте hello число экземпляров и размер для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-235">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="20a95-236">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="20a95-236">Create Application Gateway</span></span>

<span data-ttu-id="20a95-237">Создание шлюза приложения со всеми объектами конфигурации из hello в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="20a95-237">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="20a95-238">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="20a95-238">Get application gateway DNS name</span></span>

<span data-ttu-id="20a95-239">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="20a95-239">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="20a95-240">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="20a95-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="20a95-241">tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="20a95-241">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="20a95-242">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="20a95-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="20a95-243">tooconfigure hello интерфейсных IP запись CNAME, получить сведения о шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений.</span><span class="sxs-lookup"><span data-stu-id="20a95-243">tooconfigure hello frontend IP CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="20a95-244">шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME.</span><span class="sxs-lookup"><span data-stu-id="20a95-244">hello application gateway's DNS name should be used toocreate a CNAME record.</span></span> <span data-ttu-id="20a95-245">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="20a95-245">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="20a95-246">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="20a95-246">Next steps</span></span>

<span data-ttu-id="20a95-247">Если toolearn разгрузки Secure Sockets Layer (SSL), см. [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="20a95-247">If you want toolearn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

