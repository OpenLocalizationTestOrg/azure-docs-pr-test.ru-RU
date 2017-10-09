---
title: "Шлюз приложений для размещения нескольких узлов aaaCreate | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, настройте шлюз приложения Azure для размещения нескольких веб-приложений на hello одного шлюза."
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
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="66eaf-103">Создание шлюза приложений для размещения нескольких веб-приложений</span><span class="sxs-lookup"><span data-stu-id="66eaf-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="66eaf-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="66eaf-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="66eaf-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="66eaf-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="66eaf-106">Размещение нескольких сайтов позволяет toodeploy более одного веб-приложения на hello же шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="66eaf-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="66eaf-107">Он основывается на присутствие заголовка узла в hello входящего запроса HTTP, toodetermine прослушивателя, который будет получать трафик.</span><span class="sxs-lookup"><span data-stu-id="66eaf-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="66eaf-108">затем Hello прослушиватель направляет трафик tooappropriate внутреннего пула, настроенным в определение правил hello hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="66eaf-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="66eaf-109">В веб-приложениях включен протокол SSL шлюз приложений зависит от hello Указание имени сервера (SNI) расширения toochoose hello правильный прослушивателя для hello веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="66eaf-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="66eaf-110">Обычно используются для размещения нескольких сайтов — tooload балансировать нагрузку по запросам для другом доменах toodifferent серверных пулов.</span><span class="sxs-lookup"><span data-stu-id="66eaf-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="66eaf-111">Аналогичным образом несколько поддомены одного корневого домена также может быть размещена на приветствия hello же шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="66eaf-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="66eaf-112">Сценарий</span><span class="sxs-lookup"><span data-stu-id="66eaf-112">Scenario</span></span>

<span data-ttu-id="66eaf-113">В следующем примере hello, шлюз приложений обслуживает трафик для contoso.com и fabrikam.com с помощью двух серверных пулов: contoso пул серверов и fabrikam пул серверов.</span><span class="sxs-lookup"><span data-stu-id="66eaf-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="66eaf-114">Аналогичную программу установки может быть поддомены toohost используется как app.contoso.com и blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="66eaf-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="66eaf-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="66eaf-116">Before you begin</span></span>

1. <span data-ttu-id="66eaf-117">Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello.</span><span class="sxs-lookup"><span data-stu-id="66eaf-117">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="66eaf-118">Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="66eaf-118">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="66eaf-119">серверы Hello добавлены серверной части пула toouse toohello hello использование шлюза приложений должен существовать или либо в виртуальной сети hello в отдельной подсети или открытый IP/VIP-адрес, назначенный созданы их конечные точки.</span><span class="sxs-lookup"><span data-stu-id="66eaf-119">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="66eaf-120">Требования</span><span class="sxs-lookup"><span data-stu-id="66eaf-120">Requirements</span></span>

* <span data-ttu-id="66eaf-121">**Пул серверных:** hello список IP-адресов серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="66eaf-121">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="66eaf-122">Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="66eaf-122">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="66eaf-123">Можно также использовать полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="66eaf-123">FQDN can also be used.</span></span>
* <span data-ttu-id="66eaf-124">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="66eaf-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="66eaf-125">Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="66eaf-125">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="66eaf-126">**Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="66eaf-126">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="66eaf-127">Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="66eaf-127">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="66eaf-128">**Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).</span><span class="sxs-lookup"><span data-stu-id="66eaf-128">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="66eaf-129">Для шлюзов приложений с поддержкой нескольких сайтов также добавляются имя узла и индикаторы SNI.</span><span class="sxs-lookup"><span data-stu-id="66eaf-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="66eaf-130">**Правило:** правило hello привязывает hello прослушивателя, пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="66eaf-130">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="66eaf-131">Правила обрабатываются в порядке hello, в котором они перечислены, а трафик будет направляться через hello первое подходящее правило вне зависимости от точности.</span><span class="sxs-lookup"><span data-stu-id="66eaf-131">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="66eaf-132">Например при наличии правила с помощью базовых прослушивателя и правила с помощью прослушивателя несколькими сайтами обоих на hello же порт, правило hello с прослушивателя hello нескольких сайтов, необходимо указать перед hello правило с прослушивателем basic hello в порядке для hello toofunction правило нескольких сайтов, как ожидается.</span><span class="sxs-lookup"><span data-stu-id="66eaf-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="66eaf-133">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="66eaf-133">Create an application gateway</span></span>

<span data-ttu-id="66eaf-134">представлены шаги hello нужен toocreate шлюза приложения Hello:</span><span class="sxs-lookup"><span data-stu-id="66eaf-134">hello following are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="66eaf-135">Создание группы ресурсов для диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="66eaf-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="66eaf-136">Создание виртуальной сети, подсети и общедоступный IP-адрес для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="66eaf-136">Create a virtual network, subnets, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="66eaf-137">Создание объекта конфигурации шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="66eaf-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="66eaf-138">Создание ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="66eaf-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="66eaf-139">Создание группы ресурсов для диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="66eaf-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="66eaf-140">Убедитесь, что используется последняя версия Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="66eaf-140">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="66eaf-141">Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="66eaf-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="66eaf-142">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="66eaf-142">Step 1</span></span>

<span data-ttu-id="66eaf-143">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="66eaf-143">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="66eaf-144">С помощью учетных данных, запрашиваемых tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="66eaf-144">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="66eaf-145">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="66eaf-145">Step 2</span></span>

<span data-ttu-id="66eaf-146">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="66eaf-146">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="66eaf-147">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="66eaf-147">Step 3</span></span>

<span data-ttu-id="66eaf-148">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="66eaf-148">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="66eaf-149">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="66eaf-149">Step 4</span></span>

<span data-ttu-id="66eaf-150">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="66eaf-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="66eaf-151">В качестве альтернативы можно также создать теги группы ресурсов для шлюза приложений:</span><span class="sxs-lookup"><span data-stu-id="66eaf-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="66eaf-152">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="66eaf-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="66eaf-153">Это расположение используется в качестве расположения по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="66eaf-153">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="66eaf-154">Убедитесь, что все команды toocreate hello использование шлюза приложений одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="66eaf-154">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="66eaf-155">В приведенном выше примере hello, мы создали группу ресурсов под названием **appgw RG** с расположением **Запад США**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-155">In hello example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="66eaf-156">Если вам требуется пользовательский зонд tooconfigure шлюза приложения, см. раздел [создать шлюз приложений с пользовательской проверки с помощью PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="66eaf-156">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="66eaf-157">Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66eaf-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="66eaf-158">Создание виртуальной сети и подсетей</span><span class="sxs-lookup"><span data-stu-id="66eaf-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="66eaf-159">Следующий пример показывает как Hello toocreate виртуальной сети с помощью диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="66eaf-159">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="66eaf-160">На этом шаге создаются две подсети.</span><span class="sxs-lookup"><span data-stu-id="66eaf-160">Two subnets are created in this step.</span></span> <span data-ttu-id="66eaf-161">для самого шлюза приложения hello — первая подсеть Hello.</span><span class="sxs-lookup"><span data-stu-id="66eaf-161">hello first subnet is for hello application gateway itself.</span></span> <span data-ttu-id="66eaf-162">Шлюз приложений требуется собственный toohold подсети его экземпляров.</span><span class="sxs-lookup"><span data-stu-id="66eaf-162">Application gateway requires its own subnet toohold its instances.</span></span> <span data-ttu-id="66eaf-163">В этой подсети могут развертываться только другие шлюзы приложений.</span><span class="sxs-lookup"><span data-stu-id="66eaf-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="66eaf-164">второй подсеть Hello — используется toohold hello приложения внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="66eaf-164">hello second subnet is used toohold hello application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="66eaf-165">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="66eaf-165">Step 1</span></span>

<span data-ttu-id="66eaf-166">Назначьте hello адрес диапазона 10.0.0.0/24 toohello подсети переменной toobe используется toohold hello шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="66eaf-166">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toohold hello application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="66eaf-167">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="66eaf-167">Step 2</span></span>

<span data-ttu-id="66eaf-168">Назначьте hello адрес диапазона 10.0.1.0/24 toohello подсети2 переменных toobe для hello внутренних пулов.</span><span class="sxs-lookup"><span data-stu-id="66eaf-168">Assign hello address range 10.0.1.0/24 toohello subnet2 variable toobe used for hello backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="66eaf-169">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="66eaf-169">Step 3</span></span>

<span data-ttu-id="66eaf-170">Создайте виртуальную сеть с именем **appgwvnet** в группе ресурсов **appgw rg** для региона hello Запад США, с 10.0.0.0/16 hello префикс подсети 10.0.0.0/24, а 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="66eaf-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="66eaf-171">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="66eaf-171">Step 4</span></span>

<span data-ttu-id="66eaf-172">Присвоить значение переменной подсети для hello дальнейшие действия, который создает шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="66eaf-172">Assign a subnet variable for hello next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="66eaf-173">Создать общедоступный IP-адрес для интерфейса конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="66eaf-173">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="66eaf-174">Создание общих ресурсов IP **publicIP01** в группе ресурсов **appgw rg** для региона hello Запад США.</span><span class="sxs-lookup"><span data-stu-id="66eaf-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="66eaf-175">IP-адрес назначается шлюз приложений toohello при запуске службы hello.</span><span class="sxs-lookup"><span data-stu-id="66eaf-175">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="66eaf-176">Создание конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="66eaf-176">Create application gateway configuration</span></span>

<span data-ttu-id="66eaf-177">Перед созданием шлюза приложения hello имеют tooset копирование всех элементов конфигурации.</span><span class="sxs-lookup"><span data-stu-id="66eaf-177">You have tooset up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="66eaf-178">Hello следующие действия создадут hello элементы конфигурации, которые необходимы для ресурса шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="66eaf-178">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="66eaf-179">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="66eaf-179">Step 1</span></span>

<span data-ttu-id="66eaf-180">Создайте конфигурацию IP-адресов шлюза приложений с именем **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="66eaf-181">При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и маршрутизацию сетевого трафика toohello IP-адресов в пул IP-адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="66eaf-181">When application gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="66eaf-182">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="66eaf-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="66eaf-183">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="66eaf-183">Step 2</span></span>

<span data-ttu-id="66eaf-184">Настройка hello серверной части IP-адресов с именем **pool01** и **pool2** с IP-адресами **134.170.185.46**, **134.170.188.221**, **134.170.185.50** для **pool1** и **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  для **pool2**.</span><span class="sxs-lookup"><span data-stu-id="66eaf-184">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="66eaf-185">В этом примере существует два внутренней пулы tooroute трафика на основе hello запрошенного узла.</span><span class="sxs-lookup"><span data-stu-id="66eaf-185">In this example, there are two back-end pools tooroute network traffic based on hello requested site.</span></span> <span data-ttu-id="66eaf-186">Один пул принимает трафик от сайта contoso.com, а другой — от сайта fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="66eaf-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="66eaf-187">У вас есть tooreplace hello, предшествующий IP адресов tooadd собственных конечных точек приложения IP адрес.</span><span class="sxs-lookup"><span data-stu-id="66eaf-187">You have tooreplace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> <span data-ttu-id="66eaf-188">Вместо внутренних IP-адресов для серверных экземпляров можно также использовать общедоступные IP-адреса, полное доменное имя или сетевую карту виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="66eaf-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="66eaf-189">toospecify полных доменных имен, а не IP-адресов в PowerShell, используйте «-BackendFQDNs» параметра.</span><span class="sxs-lookup"><span data-stu-id="66eaf-189">toospecify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="66eaf-190">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="66eaf-190">Step 3</span></span>

<span data-ttu-id="66eaf-191">Настройка параметров шлюза приложения **poolsetting01** и **poolsetting02** hello балансировки нагрузки сетевого трафика в пуле hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="66eaf-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="66eaf-192">В этом примере вы настройки другой пул серверной части для пулов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="66eaf-192">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="66eaf-193">Для каждого пула тыловых серверов параметры можно настроить отдельно.</span><span class="sxs-lookup"><span data-stu-id="66eaf-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="66eaf-194">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="66eaf-194">Step 4</span></span>

<span data-ttu-id="66eaf-195">Настройте интерфейсный IP hello общедоступную конечную точку IP.</span><span class="sxs-lookup"><span data-stu-id="66eaf-195">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="66eaf-196">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="66eaf-196">Step 5</span></span>

<span data-ttu-id="66eaf-197">Настройте hello интерфейсный порт для шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="66eaf-197">Configure hello front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="66eaf-198">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="66eaf-198">Step 6</span></span>

<span data-ttu-id="66eaf-199">Настройте два сертификата SSL для веб-сайтов hello двух мы будем toosupport в этом примере.</span><span class="sxs-lookup"><span data-stu-id="66eaf-199">Configure two SSL certificates for hello two websites we are going toosupport in this example.</span></span> <span data-ttu-id="66eaf-200">Один сертификат является трафика contoso.com и fabrikam.com трафика hello других.</span><span class="sxs-lookup"><span data-stu-id="66eaf-200">One certificate is for contoso.com traffic and hello other is for fabrikam.com traffic.</span></span> <span data-ttu-id="66eaf-201">Это должны быть сертификаты, выданные веб-сайтам центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="66eaf-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="66eaf-202">Самозаверяющие сертификаты поддерживаются, но их не рекомендуется использовать трафика в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="66eaf-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="66eaf-203">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="66eaf-203">Step 7</span></span>

<span data-ttu-id="66eaf-204">Настройка двух прослушивателей для hello двух веб-сайтов в этом примере.</span><span class="sxs-lookup"><span data-stu-id="66eaf-204">Configure two listeners for hello two web sites in this example.</span></span> <span data-ttu-id="66eaf-205">Этот шаг позволяет настроить hello прослушиватели для открытого IP-адреса, порта и узла используется tooreceive входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="66eaf-205">This step configures hello listeners for public IP address, port, and host used tooreceive incoming traffic.</span></span> <span data-ttu-id="66eaf-206">Параметр имени узла требуется для поддержки нескольких веб-узлов и toohello соответствующий набор веб-сайт, для которого hello трафика.</span><span class="sxs-lookup"><span data-stu-id="66eaf-206">HostName parameter is required for multiple site support and should be set toohello appropriate website for which hello traffic is received.</span></span> <span data-ttu-id="66eaf-207">Параметр RequireServerNameIndication должен быть установлен tootrue веб-сайтах, требуется поддержка протокола SSL в случае нескольких узлов.</span><span class="sxs-lookup"><span data-stu-id="66eaf-207">RequireServerNameIndication parameter should be set tootrue for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="66eaf-208">Если требуется поддержка протокола SSL, необходимо также toospecify hello SSL сертификат, используемый toosecure трафика для этого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="66eaf-208">If SSL support is required, you also need toospecify hello SSL certificate that is used toosecure traffic for that web application.</span></span> <span data-ttu-id="66eaf-209">сочетание Hello FrontendIPConfiguration, FrontendPort и имя узла должно быть уникальным tooa прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="66eaf-209">hello combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique tooa listener.</span></span> <span data-ttu-id="66eaf-210">Каждый прослушиватель может поддерживать один сертификат.</span><span class="sxs-lookup"><span data-stu-id="66eaf-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="66eaf-211">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="66eaf-211">Step 8</span></span>

<span data-ttu-id="66eaf-212">Создайте два правила, задание для hello два веб-приложений в этом примере.</span><span class="sxs-lookup"><span data-stu-id="66eaf-212">Create two rule setting for hello two web applications in this example.</span></span> <span data-ttu-id="66eaf-213">Правило объединяет прослушиватели, серверные пулы и параметры протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="66eaf-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="66eaf-214">Этот шаг позволяет настроить hello приложения шлюза toouse основные правила маршрутизации, один для каждого веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="66eaf-214">This step configures hello application gateway toouse Basic routing rule, one for each website.</span></span> <span data-ttu-id="66eaf-215">Веб-сайт tooeach трафик полученных его настроенного прослушивателя и перенаправляться tooits настройки внутреннего пула, с помощью свойства hello, указанные в hello BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="66eaf-215">Traffic tooeach website is received by its configured listener, and is then directed tooits configured backend pool, using hello properties specified in hello BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="66eaf-216">Шаг 9.</span><span class="sxs-lookup"><span data-stu-id="66eaf-216">Step 9</span></span>

<span data-ttu-id="66eaf-217">Настройте hello число экземпляров и размер для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="66eaf-217">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="66eaf-218">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="66eaf-218">Create application gateway</span></span>

<span data-ttu-id="66eaf-219">Создание шлюза приложения со всеми объектами конфигурации из hello в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="66eaf-219">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="66eaf-220">Подготовка шлюза приложения — это длительная операция и может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="66eaf-220">Application Gateway provisioning is a long running operation and may take some time toocomplete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="66eaf-221">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="66eaf-221">Get application gateway DNS name</span></span>

<span data-ttu-id="66eaf-222">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="66eaf-222">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="66eaf-223">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="66eaf-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="66eaf-224">tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="66eaf-224">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="66eaf-225">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="66eaf-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="66eaf-226">toodo сведения, получение шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений.</span><span class="sxs-lookup"><span data-stu-id="66eaf-226">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="66eaf-227">шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="66eaf-227">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="66eaf-228">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="66eaf-228">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="66eaf-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66eaf-229">Next steps</span></span>

<span data-ttu-id="66eaf-230">Узнайте, как tooprotect веб-сайты с [шлюз приложений - брандмауэр веб-приложения](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="66eaf-230">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

