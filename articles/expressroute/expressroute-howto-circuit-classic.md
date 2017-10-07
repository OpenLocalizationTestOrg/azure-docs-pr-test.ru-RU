---
title: "Создание и изменение канала ExpressRoute с помощью PowerShell и классического портала Azure | Документация Майкрософт"
description: "В этой статье содержится описание этапов hello для создания и подготовки канал ExpressRoute. В этой статье также показано, как состояние toocheck hello, обновить, или удалить и Отмена подготовки к схемы."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="26226-104">Создание и изменение канала ExpressRoute с помощью PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="26226-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="26226-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="26226-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="26226-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26226-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="26226-107">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="26226-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="26226-108">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="26226-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="26226-109">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="26226-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="26226-110">В этой статье описывается toocreate действия hello канал Azure ExpressRoute с помощью PowerShell командлеты и hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="26226-110">This article walks you through hello steps toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello classic deployment model.</span></span> <span data-ttu-id="26226-111">В этой статье также показано, как состояние toocheck hello, обновить, или удалить и отзыв канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="26226-111">This article also shows you how toocheck hello status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="26226-112">**О моделях развертывания Azure**</span><span class="sxs-lookup"><span data-stu-id="26226-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="26226-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="26226-113">Before you begin</span></span>
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a><span data-ttu-id="26226-114">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="26226-114">Step 1.</span></span> <span data-ttu-id="26226-115">Проверьте предварительные условия hello и статей рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="26226-115">Review hello prerequisites and workflow articles</span></span>
<span data-ttu-id="26226-116">Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="26226-116">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="26226-117">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="26226-117">Step 2.</span></span> <span data-ttu-id="26226-118">Установить последние версии hello hello модули PowerShell службы управления Azure (SM)</span><span class="sxs-lookup"><span data-stu-id="26226-118">Install hello latest versions of hello Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="26226-119">Следуйте инструкциям в разделе hello [Приступая к работе с помощью командлетов Azure PowerShell](/powershell/azure/overview) пошаговые инструкции о том, как tooconfigure модули Azure PowerShell hello toouse компьютера.</span><span class="sxs-lookup"><span data-stu-id="26226-119">Follow hello instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="26226-120">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="26226-120">Step 3.</span></span> <span data-ttu-id="26226-121">Войдите в tooyour учетная запись Azure и выберите подписку</span><span class="sxs-lookup"><span data-stu-id="26226-121">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="26226-122">Откройте консоль PowerShell с повышенными правами и подключите tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="26226-122">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="26226-123">Используйте следующий пример toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="26226-123">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="26226-124">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="26226-124">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="26226-125">При наличии нескольких подписок выберите подписку hello, что требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="26226-125">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="26226-126">Затем используйте следующий командлет tooadd hello tooPowerShell вашей подписки Azure для hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="26226-126">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="26226-127">Создание и предоставление канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26226-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a><span data-ttu-id="26226-128">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="26226-128">Step 1.</span></span> <span data-ttu-id="26226-129">Импортируйте модули PowerShell hello для ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26226-129">Import hello PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="26226-130">Если вы еще не сделали необходимо импортировать модули hello Azure и ExpressRoute в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="26226-130">If you have not already done so, you must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="26226-131">Импортируйте модули hello hello расположение, которое они были установлены tooon локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="26226-131">You import hello modules from hello location that they were installed tooon your local computer.</span></span> <span data-ttu-id="26226-132">В зависимости от метода hello использовалась tooinstall hello модули, hello расположение может отличаться от следующих примере hello.</span><span class="sxs-lookup"><span data-stu-id="26226-132">Depending on hello method you used tooinstall hello modules, hello location may be different than hello following example shows.</span></span> <span data-ttu-id="26226-133">При необходимости измените пример hello.</span><span class="sxs-lookup"><span data-stu-id="26226-133">Modify hello example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="26226-134">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="26226-134">Step 2.</span></span> <span data-ttu-id="26226-135">Получить список поддерживаемых поставщиков, расположений и полос пропускания hello</span><span class="sxs-lookup"><span data-stu-id="26226-135">Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="26226-136">Прежде чем создавать канал ExpressRoute, необходимо hello список поставщиков поддерживаемых соединений, расположений и полосы пропускания.</span><span class="sxs-lookup"><span data-stu-id="26226-136">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="26226-137">Здравствуйте, командлета PowerShell `Get-AzureDedicatedCircuitServiceProvider` возвращает эту информацию, которая будет использоваться на последующих этапах:</span><span class="sxs-lookup"><span data-stu-id="26226-137">hello PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="26226-138">Проверьте toosee, если поставщиком соединения существует в списке.</span><span class="sxs-lookup"><span data-stu-id="26226-138">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="26226-139">Запишите hello следующую информацию, так как потребуется позднее при создании канала:</span><span class="sxs-lookup"><span data-stu-id="26226-139">Make a note of hello following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="26226-140">Имя</span><span class="sxs-lookup"><span data-stu-id="26226-140">Name</span></span>
* <span data-ttu-id="26226-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="26226-141">PeeringLocations</span></span>
* <span data-ttu-id="26226-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="26226-142">BandwidthsOffered</span></span>

<span data-ttu-id="26226-143">Теперь вы готовы toocreate канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="26226-143">You're now ready toocreate an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="26226-144">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="26226-144">Step 3.</span></span> <span data-ttu-id="26226-145">Создание канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26226-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="26226-146">Привет, в следующем примере показано, как circuit toocreate ExpressRoute 200 Мбит/с до Equinix в Силиконовой долине.</span><span class="sxs-lookup"><span data-stu-id="26226-146">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="26226-147">Если вы используете другой поставщик и другие параметры, подставьте в запрос соответствующие данные.</span><span class="sxs-lookup"><span data-stu-id="26226-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26226-148">Ваш канал ExpressRoute будет записана с момента hello выдачи ключа службы.</span><span class="sxs-lookup"><span data-stu-id="26226-148">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="26226-149">Убедитесь, что эта операция при готовности tooprovision hello цепи hello поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="26226-149">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="26226-150">Hello ниже приведен пример запроса нового ключа службы.</span><span class="sxs-lookup"><span data-stu-id="26226-150">hello following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="26226-151">Или, если вы хотите toocreate канал ExpressRoute с надстройками "премиум" hello, hello используйте следующий пример.</span><span class="sxs-lookup"><span data-stu-id="26226-151">Or, if you want toocreate an ExpressRoute circuit with hello premium add-on, use hello following example.</span></span> <span data-ttu-id="26226-152">См. toohello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md) Дополнительные сведения о премиальное дополнение hello.</span><span class="sxs-lookup"><span data-stu-id="26226-152">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more details about hello premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="26226-153">Hello ответ будет содержать hello ключа службы.</span><span class="sxs-lookup"><span data-stu-id="26226-153">hello response will contain hello service key.</span></span> <span data-ttu-id="26226-154">Подробное описание всех параметров hello можно получить, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="26226-154">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a><span data-ttu-id="26226-155">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="26226-155">Step 4.</span></span> <span data-ttu-id="26226-156">Перечислены все каналы ExpressRoute hello</span><span class="sxs-lookup"><span data-stu-id="26226-156">List all hello ExpressRoute circuits</span></span>
<span data-ttu-id="26226-157">Можно запустить hello `Get-AzureDedicatedCircuit` tooget список всех hello каналы ExpressRoute, созданные команды:</span><span class="sxs-lookup"><span data-stu-id="26226-157">You can run hello `Get-AzureDedicatedCircuit` command tooget a list of all hello ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="26226-158">Hello ответ будет что-нибудь подобное toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="26226-158">hello response will be something similar toohello following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="26226-159">Эти сведения в любое время можно получить с помощью hello `Get-AzureDedicatedCircuit` командлета.</span><span class="sxs-lookup"><span data-stu-id="26226-159">You can retrieve this information at any time by using hello `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="26226-160">Делая hello вызова без параметров перечисляет все каналы hello.</span><span class="sxs-lookup"><span data-stu-id="26226-160">Making hello call without any parameters lists all hello circuits.</span></span> <span data-ttu-id="26226-161">Ключ службы будут перечислены в hello *ServiceKey* поля.</span><span class="sxs-lookup"><span data-stu-id="26226-161">Your service key will be listed in hello *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="26226-162">Подробное описание всех параметров hello можно получить, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="26226-162">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="26226-163">Шаг 5.</span><span class="sxs-lookup"><span data-stu-id="26226-163">Step 5.</span></span> <span data-ttu-id="26226-164">Отправка ключа tooyour подключения hello службы поставщика для подготовки</span><span class="sxs-lookup"><span data-stu-id="26226-164">Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="26226-165">*ServiceProviderProvisioningState* предоставляет сведения о hello текущее состояние подготовки на стороне поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="26226-165">*ServiceProviderProvisioningState* provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="26226-166">*Состояние* предоставляет hello состояния на стороне Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="26226-166">*Status* provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="26226-167">Дополнительные сведения о состояния подготовки схемы см. в разделе hello [рабочих процессов](expressroute-workflows.md#expressroute-circuit-provisioning-states) статьи.</span><span class="sxs-lookup"><span data-stu-id="26226-167">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="26226-168">При создании нового канала ExpressRoute hello схемы будут иметь hello следующие состояния:</span><span class="sxs-lookup"><span data-stu-id="26226-168">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="26226-169">Hello канала будет отправлена toohello при поставщика услуг подключения hello находится в процессе hello включить его для вас следующие состояния:</span><span class="sxs-lookup"><span data-stu-id="26226-169">hello circuit will go toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="26226-170">Канал ExpressRoute должна иметь следующие состояния для вас toobe может toouse hello его:</span><span class="sxs-lookup"><span data-stu-id="26226-170">An ExpressRoute circuit must be in hello following state for you toobe able toouse it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="26226-171">Шаг 6.</span><span class="sxs-lookup"><span data-stu-id="26226-171">Step 6.</span></span> <span data-ttu-id="26226-172">Периодически Проверьте состояние hello и состояние hello ключа канала hello</span><span class="sxs-lookup"><span data-stu-id="26226-172">Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="26226-173">Это позволяет узнать, когда поставщик включил ваш канал.</span><span class="sxs-lookup"><span data-stu-id="26226-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="26226-174">После настройки канала hello *ServiceProviderProvisioningState* будет отображаться как *инициализировано* как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="26226-174">After hello circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in hello following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="26226-175">Шаг 7.</span><span class="sxs-lookup"><span data-stu-id="26226-175">Step 7.</span></span> <span data-ttu-id="26226-176">Создание конфигурации маршрутизации</span><span class="sxs-lookup"><span data-stu-id="26226-176">Create your routing configuration</span></span>
<span data-ttu-id="26226-177">Ссылки toohello [expressroute в конфигурацию маршрутизации (Создание и изменение схемы пиринги)](expressroute-howto-routing-classic.md) статьи для получения пошаговых инструкций.</span><span class="sxs-lookup"><span data-stu-id="26226-177">Refer toohello [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26226-178">Эти инструкции применяются только toocircuits, созданных с помощью службы поставщиков, предлагающих услуги подключений второго уровня.</span><span class="sxs-lookup"><span data-stu-id="26226-178">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="26226-179">Если вы работаете с поставщиком, предлагающим услуги третьего уровня (обычно это IPVPN, например MPLS), то ваш поставщик услуг подключения выполнит настройку и управление конфигурацией самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="26226-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="26226-180">Шаг 8.</span><span class="sxs-lookup"><span data-stu-id="26226-180">Step 8.</span></span> <span data-ttu-id="26226-181">Связывание виртуальной сети tooan канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26226-181">Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="26226-182">Затем свяжите виртуальной сети tooyour канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="26226-182">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="26226-183">См. слишком[ExpressRoute связывания каналов сетей toovirtual](expressroute-howto-linkvnet-classic.md) пошаговые инструкции.</span><span class="sxs-lookup"><span data-stu-id="26226-183">Refer too[Linking ExpressRoute circuits toovirtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="26226-184">Получить виртуальные сети с помощью hello классической модели развертывания для ExpressRoute toocreate [Создание виртуальной сети для ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="26226-184">If you need toocreate a virtual network using hello classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="26226-185">Получение состояния hello канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26226-185">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="26226-186">Эти сведения в любое время можно получить с помощью hello `Get-AzureCircuit` командлета.</span><span class="sxs-lookup"><span data-stu-id="26226-186">You can retrieve this information at any time by using hello `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="26226-187">Делая hello вызова без параметров перечисляет все каналы hello.</span><span class="sxs-lookup"><span data-stu-id="26226-187">Making hello call without any parameters lists all hello circuits.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="26226-188">Сведения о конкретных канал ExpressRoute можно получить, передав в качестве параметра вызова toohello hello ключа службы.</span><span class="sxs-lookup"><span data-stu-id="26226-188">You can get information on a specific ExpressRoute circuit by passing hello service key as a parameter toohello call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="26226-189">Подробное описание всех параметров hello можно получить, выполнив следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="26226-189">You can get detailed descriptions of all hello parameters by running hello following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="26226-190">Изменение канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26226-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="26226-191">Некоторые свойства канала ExpressRoute можно изменить, не повлияв на подключение.</span><span class="sxs-lookup"><span data-stu-id="26226-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="26226-192">Можно сделать hello без простоев следующие:</span><span class="sxs-lookup"><span data-stu-id="26226-192">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="26226-193">включать и отключать надстройку ExpressRoute "Премиум" для канала ExpressRoute;</span><span class="sxs-lookup"><span data-stu-id="26226-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="26226-194">Увеличение hello пропускной способностью вашего канала ExpressRoute при условии, что доступно емкости на порту hello.</span><span class="sxs-lookup"><span data-stu-id="26226-194">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="26226-195">Обратите внимание, что понижение уровня полосы пропускания канала hello не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="26226-195">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="26226-196">Изменение плана на основе данных, измеряемые tooUnlimited данных отслеживания использования hello.</span><span class="sxs-lookup"><span data-stu-id="26226-196">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="26226-197">Обратите внимание, изменяющихся план контроля использования программных продуктов hello из данных tooMetered данных не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="26226-197">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="26226-198">Параметр *Allow Classic Operations*(Разрешить классические операции) можно включать и отключать.</span><span class="sxs-lookup"><span data-stu-id="26226-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="26226-199">См. toohello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md) Дополнительные сведения об ограничениях и ограничениях.</span><span class="sxs-lookup"><span data-stu-id="26226-199">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="26226-200">tooenable hello ExpressRoute премиальное дополнение</span><span class="sxs-lookup"><span data-stu-id="26226-200">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="26226-201">Премиальное дополнение hello ExpressRoute можно включить для вашей существующей цепи с помощью hello, выполнив командлет PowerShell:</span><span class="sxs-lookup"><span data-stu-id="26226-201">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="26226-202">Ваш канал получают hello ExpressRoute premium дополнительные возможности.</span><span class="sxs-lookup"><span data-stu-id="26226-202">Your circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="26226-203">Обратите внимание, что мы начнем выставления счетов для hello premium дополнительные возможности, как только команда hello успешно запущена.</span><span class="sxs-lookup"><span data-stu-id="26226-203">Note that we will start billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="26226-204">toodisable hello ExpressRoute премиальное дополнение</span><span class="sxs-lookup"><span data-stu-id="26226-204">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="26226-205">Эта операция может завершиться ошибкой, если вы используете ресурсы, которые больше, чем то, что разрешено для стандартной схемы hello.</span><span class="sxs-lookup"><span data-stu-id="26226-205">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="26226-206">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="26226-206">Considerations</span></span>

* <span data-ttu-id="26226-207">Необходимо убедиться, hello число цепи связанных toohello виртуальных сетей находится меньше 10, прежде чем понизить из premium toostandard.</span><span class="sxs-lookup"><span data-stu-id="26226-207">You must ensure that hello number of virtual networks linked toohello circuit is less than 10 before you downgrade from premium toostandard.</span></span> <span data-ttu-id="26226-208">Если этого не сделать, ваш запрос на обновление завершится ошибкой, и вы будете по документу hello премиум-уровень.</span><span class="sxs-lookup"><span data-stu-id="26226-208">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="26226-209">Все связи с виртуальными сетями в других геополитических регионах необходимо разорвать.</span><span class="sxs-lookup"><span data-stu-id="26226-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="26226-210">Если этого не сделать, ваш запрос на обновление завершится ошибкой, и вы будете по документу hello премиум-уровень.</span><span class="sxs-lookup"><span data-stu-id="26226-210">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="26226-211">Для частного пиринга таблица маршрутов должна содержать менее 4000 маршрутов.</span><span class="sxs-lookup"><span data-stu-id="26226-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="26226-212">Если размер таблицы маршрутов больше 4000 маршрутов, сеанс BGP hello приведет к удалению и не будет снова включено, пока hello число префиксов, объявленных становится меньше 4 000.</span><span class="sxs-lookup"><span data-stu-id="26226-212">If your route table size is greater than 4,000 routes, hello BGP session will drop and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-hello-premium-add-on"></a><span data-ttu-id="26226-213">Отключить надстройку premium hello</span><span class="sxs-lookup"><span data-stu-id="26226-213">Disable hello premium add-on</span></span>
<span data-ttu-id="26226-214">Премиальное дополнение hello ExpressRoute для вашей существующей схемы, можно отключить с помощью hello, выполнив командлет PowerShell:</span><span class="sxs-lookup"><span data-stu-id="26226-214">You can disable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="26226-215">пропускная способность контура tooupdate hello ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26226-215">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="26226-216">Проверьте hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md) для поддерживаемых вариантов пропускной способности для поставщика.</span><span class="sxs-lookup"><span data-stu-id="26226-216">Check hello [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="26226-217">Можно выбрать любого размера, больше, чем размер hello вашей существующей цепи при условии, что позволяет физическому порту hello (на котором создается ваш канал).</span><span class="sxs-lookup"><span data-stu-id="26226-217">You can pick any size that is greater than hello size of your existing circuit as long as hello physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26226-218">Канал ExpressRoute toorecreate hello возможно, если имеется существующий порт hello недостаточной мощности.</span><span class="sxs-lookup"><span data-stu-id="26226-218">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="26226-219">Обновление схемы hello невозможно, если доступна без дополнительной емкости в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="26226-219">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="26226-220">Нельзя уменьшить hello пропускной способности канала ExpressRoute без прерывания.</span><span class="sxs-lookup"><span data-stu-id="26226-220">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="26226-221">Понижение уровня полосы пропускания необходимо канал ExpressRoute toodeprovision hello и повторной инициализации новый канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="26226-221">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="26226-222">Изменение размера канала</span><span class="sxs-lookup"><span data-stu-id="26226-222">Resize a circuit</span></span>

<span data-ttu-id="26226-223">После определения размера необходимо, можно использовать следующие команды tooresize hello ваш канал:</span><span class="sxs-lookup"><span data-stu-id="26226-223">After you decide what size you need, you can use hello following command tooresize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="26226-224">Будут, ваш канал был размера на стороне Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="26226-224">Your circuit will have been sized up on hello Microsoft side.</span></span> <span data-ttu-id="26226-225">Необходимо обратиться к настройки подключения поставщика tooupdate на своей стороне toomatch это изменение.</span><span class="sxs-lookup"><span data-stu-id="26226-225">You must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="26226-226">Обратите внимание, что мы начнем выставления счетов за hello обновлен параметр пропускной способности из этой точки.</span><span class="sxs-lookup"><span data-stu-id="26226-226">Note that we will start billing you for hello updated bandwidth option from this point on.</span></span>

<span data-ttu-id="26226-227">Если появится следующая ошибка при увеличении пропускной способности канала hello hello, это означает наличие остается достаточная полоса пропускания hello физического порта, где создается вашей существующей цепи.</span><span class="sxs-lookup"><span data-stu-id="26226-227">If you see hello following error when increasing hello circuit bandwidth, it means there is no sufficient bandwidth left on hello physical port where your existing circuit is created.</span></span> <span data-ttu-id="26226-228">Вы toodelete этой цепи и создайте новый канал hello размера, что нужно.</span><span class="sxs-lookup"><span data-stu-id="26226-228">You have toodelete this circuit and create a new circuit of hello size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="26226-229">Отзыв и удаление канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26226-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="26226-230">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="26226-230">Considerations</span></span>

* <span data-ttu-id="26226-231">Необходимо удалить связь всех виртуальных сетей с каналом expressroute для этой операции toosucceed hello.</span><span class="sxs-lookup"><span data-stu-id="26226-231">You must unlink all virtual networks from hello ExpressRoute circuit for this operation toosucceed.</span></span> <span data-ttu-id="26226-232">Проверьте toosee, если у вас есть все виртуальные сети, связанным toohello канала, если операция завершается неудачно.</span><span class="sxs-lookup"><span data-stu-id="26226-232">Check toosee if you have any virtual networks that are linked toohello circuit if this operation fails.</span></span>
* <span data-ttu-id="26226-233">Если состояние подготовки службы поставщика hello ExpressRoute канала **Provisioning** или **инициализировано** необходимо работать с ваш канал hello toodeprovision поставщика службы с их стороны.</span><span class="sxs-lookup"><span data-stu-id="26226-233">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="26226-234">Она будет продолжать tooreserve ресурсы и выставлять вам счет на поставщика услуг hello завершения списания цепи hello и уведомляет нас.</span><span class="sxs-lookup"><span data-stu-id="26226-234">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="26226-235">Если поставщик услуг hello отозваны hello канала (состояние подготовки поставщика услуг hello задано слишком**не инициализировано**) можно удалить цепь hello.</span><span class="sxs-lookup"><span data-stu-id="26226-235">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="26226-236">Это остановит выставления счетов для hello схемы.</span><span class="sxs-lookup"><span data-stu-id="26226-236">This will stop billing for hello circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="26226-237">Удаление канала</span><span class="sxs-lookup"><span data-stu-id="26226-237">Delete a circuit</span></span>

<span data-ttu-id="26226-238">Ваш канал ExpressRoute можно удалить, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="26226-238">You can delete your ExpressRoute circuit by running hello following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="26226-239">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="26226-239">Next steps</span></span>
<span data-ttu-id="26226-240">После создания ваш канал, убедитесь, что hello следующие:</span><span class="sxs-lookup"><span data-stu-id="26226-240">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="26226-241">Создание и изменение маршрутизации для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26226-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="26226-242">Связать вашей виртуальной сети tooyour канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26226-242">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

