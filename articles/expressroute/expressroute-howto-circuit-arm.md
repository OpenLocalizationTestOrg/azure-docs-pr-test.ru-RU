---
title: "Создание и изменение канала ExpressRoute с помощью PowerShell и Azure Resource Manager | Документация Майкрософт"
description: "В этой статье описывается, как toocreate, подготовки, проверьте, обновление, удаление и отзыв канал ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="1f810-103">Создание и изменение канала ExpressRoute с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f810-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f810-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="1f810-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="1f810-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f810-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="1f810-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="1f810-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="1f810-107">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="1f810-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="1f810-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="1f810-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="1f810-109">В этой статье описывается, как circuit toocreate Azure ExpressRoute с помощью PowerShell командлеты и hello Azure модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1f810-109">This article describes how toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="1f810-110">В этой статье также рассказывается, как toocheck hello состояние канала hello, обновления или удаления и сделать.</span><span class="sxs-lookup"><span data-stu-id="1f810-110">This article also shows you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1f810-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="1f810-111">Before you begin</span></span>
* <span data-ttu-id="1f810-112">Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="1f810-112">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="1f810-113">Дополнительные сведения см. в [обзоре Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1f810-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="1f810-114">Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="1f810-114">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="1f810-115">Создание и предоставление канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1f810-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="1f810-116">1. Войдите в tooyour учетная запись Azure и выберите подписку</span><span class="sxs-lookup"><span data-stu-id="1f810-116">1. Sign in tooyour Azure account and select your subscription</span></span>
<span data-ttu-id="1f810-117">toobegin конфигурацию входа tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="1f810-117">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="1f810-118">Используйте следующие примеры toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-118">Use hello following examples toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="1f810-119">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-119">Check hello subscriptions for hello account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="1f810-120">Выберите подписку hello toocreate expressroute в для:</span><span class="sxs-lookup"><span data-stu-id="1f810-120">Select hello subscription that you want toocreate an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="1f810-121">2. Получить список поддерживаемых поставщиков, расположений и полос пропускания hello</span><span class="sxs-lookup"><span data-stu-id="1f810-121">2. Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="1f810-122">Прежде чем создавать канал ExpressRoute, необходимо hello список поставщиков поддерживаемых соединений, расположений и полосы пропускания.</span><span class="sxs-lookup"><span data-stu-id="1f810-122">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="1f810-123">Здравствуйте, командлета PowerShell **Get AzureRmExpressRouteServiceProvider** возвращает эту информацию, которая будет использоваться на последующих этапах:</span><span class="sxs-lookup"><span data-stu-id="1f810-123">hello PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="1f810-124">Проверьте toosee, если поставщиком соединения существует в списке.</span><span class="sxs-lookup"><span data-stu-id="1f810-124">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="1f810-125">Запишите hello следующую информацию.</span><span class="sxs-lookup"><span data-stu-id="1f810-125">Make a note of hello following information.</span></span> <span data-ttu-id="1f810-126">Они потребуется позже при создании канала.</span><span class="sxs-lookup"><span data-stu-id="1f810-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="1f810-127">Имя</span><span class="sxs-lookup"><span data-stu-id="1f810-127">Name</span></span>
* <span data-ttu-id="1f810-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="1f810-128">PeeringLocations</span></span>
* <span data-ttu-id="1f810-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="1f810-129">BandwidthsOffered</span></span>

<span data-ttu-id="1f810-130">Теперь вы готовы toocreate канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1f810-130">You're now ready toocreate an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="1f810-131">3. Создание канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1f810-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="1f810-132">Перед созданием канала ExpressRoute необходимо создать группу ресурсов (если вы этого еще не сделали)</span><span class="sxs-lookup"><span data-stu-id="1f810-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="1f810-133">Это можно сделать, запустив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1f810-133">You can do so by running hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="1f810-134">Привет, в следующем примере показано, как circuit toocreate ExpressRoute 200 Мбит/с до Equinix в Силиконовой долине.</span><span class="sxs-lookup"><span data-stu-id="1f810-134">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="1f810-135">Если вы используете другой поставщик и другие параметры, подставьте в запрос соответствующие данные.</span><span class="sxs-lookup"><span data-stu-id="1f810-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="1f810-136">Hello ниже приведен пример запроса нового ключа службы.</span><span class="sxs-lookup"><span data-stu-id="1f810-136">hello following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="1f810-137">Убедитесь, что указан правильный уровень номера SKU hello и семейство номеров SKU:</span><span class="sxs-lookup"><span data-stu-id="1f810-137">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="1f810-138">Уровень SKU определяет, какая надстройка включена — ExpressRoute Standard или ExpressRoute Premium.</span><span class="sxs-lookup"><span data-stu-id="1f810-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="1f810-139">Можно указать *Стандартная* tooget hello стандартном номере SKU или *Premium* hello premium надстройки.</span><span class="sxs-lookup"><span data-stu-id="1f810-139">You can specify *Standard* tooget hello standard SKU or *Premium* for hello premium add-on.</span></span>
* <span data-ttu-id="1f810-140">Семейство номеров SKU определяет hello выставления счетов с типом.</span><span class="sxs-lookup"><span data-stu-id="1f810-140">SKU family determines hello billing type.</span></span> <span data-ttu-id="1f810-141">Выберите *Metereddata* для тарифного плана с оплатой за трафик или *Unlimiteddata* для безлимитного тарифного плана.</span><span class="sxs-lookup"><span data-stu-id="1f810-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="1f810-142">Можно изменить тип выставления счетов hello из *Metereddata* слишком*Unlimiteddata*, но не может изменить тип hello из *Unlimiteddata* слишком*Metereddata* .</span><span class="sxs-lookup"><span data-stu-id="1f810-142">You can change hello billing type from *Metereddata* too*Unlimiteddata*, but you can't change hello type from *Unlimiteddata* too*Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f810-143">Ваш канал ExpressRoute будет записана с момента hello выдачи ключа службы.</span><span class="sxs-lookup"><span data-stu-id="1f810-143">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="1f810-144">Убедитесь, что эта операция при готовности tooprovision hello цепи hello поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="1f810-144">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="1f810-145">Hello ответ содержит ключ службы hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-145">hello response contains hello service key.</span></span> <span data-ttu-id="1f810-146">Подробное описание всех параметров hello можно получить, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="1f810-146">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="1f810-147">4. Получение списка всех каналов ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1f810-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="1f810-148">список всех hello каналы ExpressRoute, которые были созданы tooget запуска hello **Get AzureRmExpressRouteCircuit** команды:</span><span class="sxs-lookup"><span data-stu-id="1f810-148">tooget a list of all hello ExpressRoute circuits that you created, run hello **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="1f810-149">Hello ответа будет выглядеть аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1f810-149">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

<span data-ttu-id="1f810-150">Эти сведения в любое время можно получить с помощью hello `Get-AzureRmExpressRouteCircuit` командлета.</span><span class="sxs-lookup"><span data-stu-id="1f810-150">You can retrieve this information at any time by using hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="1f810-151">Делая hello вызова без параметров перечисляет все каналы hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-151">Making hello call with no parameters lists all hello circuits.</span></span> <span data-ttu-id="1f810-152">Ключ службы будут перечислены в hello *ServiceKey* поля:</span><span class="sxs-lookup"><span data-stu-id="1f810-152">Your service key will be listed in hello *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="1f810-153">Hello ответа будет выглядеть аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1f810-153">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="1f810-154">Подробное описание всех параметров hello можно получить, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="1f810-154">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="1f810-155">5. Отправка ключа tooyour подключения hello службы поставщика для подготовки</span><span class="sxs-lookup"><span data-stu-id="1f810-155">5. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="1f810-156">*ServiceProviderProvisioningState* предоставляет сведения о текущем состоянии hello подготовки на стороне поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-156">*ServiceProviderProvisioningState* provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="1f810-157">Состояния содержит состояние hello hello стороны Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="1f810-157">Status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="1f810-158">Дополнительные сведения о состояния подготовки схемы см. в разделе hello [рабочих процессов](expressroute-workflows.md#expressroute-circuit-provisioning-states) статьи.</span><span class="sxs-lookup"><span data-stu-id="1f810-158">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="1f810-159">При создании нового канала ExpressRoute hello схемы будут иметь hello следующие состояния:</span><span class="sxs-lookup"><span data-stu-id="1f810-159">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="1f810-160">цепь Hello приведет к изменению toohello при поставщика услуг подключения hello находится в процессе hello включить его для вас следующие состояния:</span><span class="sxs-lookup"><span data-stu-id="1f810-160">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="1f810-161">Для вас toobe может toouse канал ExpressRoute он должен быть в hello следующие состояния:</span><span class="sxs-lookup"><span data-stu-id="1f810-161">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="1f810-162">6. Периодически Проверьте состояние hello и состояние hello ключа канала hello</span><span class="sxs-lookup"><span data-stu-id="1f810-162">6. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="1f810-163">Проверка состояния hello и состояние hello hello ключа канала позволяет узнать, когда поставщик подключит ваш канал.</span><span class="sxs-lookup"><span data-stu-id="1f810-163">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="1f810-164">После настройки канала hello *ServiceProviderProvisioningState* отображается как *инициализировано*, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="1f810-164">After hello circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in hello following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="1f810-165">Hello ответа будет выглядеть аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1f810-165">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                       }
    ServiceKey                       : **************************************
    Peerings                         : []

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="1f810-166">7. Создание конфигурации маршрутизации</span><span class="sxs-lookup"><span data-stu-id="1f810-166">7. Create your routing configuration</span></span>
<span data-ttu-id="1f810-167">Пошаговые инструкции см. в разделе hello [expressroute в конфигурацию маршрутизации](expressroute-howto-routing-arm.md) статью toocreate и изменения пиринги в цепи.</span><span class="sxs-lookup"><span data-stu-id="1f810-167">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f810-168">Эти инструкции применяются только toocircuits, созданных с помощью службы поставщиков, предлагающих услуги подключений второго уровня.</span><span class="sxs-lookup"><span data-stu-id="1f810-168">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="1f810-169">Если вы работаете с поставщиком, предлагающим услуги третьего уровня (обычно это IPVPN, например MPLS), то ваш поставщик услуг подключения выполнит настройку и управление конфигурацией самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="1f810-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="1f810-170">8. Связывание виртуальной сети tooan канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1f810-170">8. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="1f810-171">Затем свяжите виртуальной сети tooyour канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1f810-171">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="1f810-172">Используйте hello [связывание виртуальной сети цепи tooExpressRoute](expressroute-howto-linkvnet-arm.md) статьи при работе с моделью развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-172">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="1f810-173">Получение состояния hello канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1f810-173">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="1f810-174">Эти сведения в любое время можно получить с помощью hello **Get AzureRmExpressRouteCircuit** командлета.</span><span class="sxs-lookup"><span data-stu-id="1f810-174">You can retrieve this information at any time by using hello **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="1f810-175">Делая hello вызова без параметров перечисляет все каналы hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-175">Making hello call with no parameters lists all hello circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="1f810-176">Hello ответ будет иметь примерно toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1f810-176">hello response will be similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                            "ServiceProviderName": "Equinix",
                                            "PeeringLocation": "Silicon Valley",
                                            "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="1f810-177">Сведения о конкретных канал ExpressRoute можно получить, передав имя группы ресурсов hello и имя схемы как вызов toohello параметр:</span><span class="sxs-lookup"><span data-stu-id="1f810-177">You can get information on a specific ExpressRoute circuit by passing hello resource group name and circuit name as a parameter toohello call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="1f810-178">Hello ответа будет выглядеть аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1f810-178">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                            "Tier": "Standard",
                                            "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="1f810-179">Подробное описание всех параметров hello можно получить, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="1f810-179">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="1f810-180"><a name="modify"></a>Изменение канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1f810-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="1f810-181">Некоторые свойства канала ExpressRoute можно изменить, не повлияв на подключение.</span><span class="sxs-lookup"><span data-stu-id="1f810-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="1f810-182">Можно сделать hello без простоев следующие:</span><span class="sxs-lookup"><span data-stu-id="1f810-182">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="1f810-183">включать и отключать надстройку ExpressRoute "Премиум" для канала ExpressRoute;</span><span class="sxs-lookup"><span data-stu-id="1f810-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="1f810-184">Увеличение hello пропускной способностью вашего канала ExpressRoute при условии, что доступно емкости на порту hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-184">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="1f810-185">Понижение уровня полосы пропускания канала hello не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="1f810-185">Downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="1f810-186">Изменение плана на основе данных, измеряемые tooUnlimited данных отслеживания использования hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-186">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="1f810-187">Изменение hello измерения план из данных tooMetered данных не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="1f810-187">Changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="1f810-188">Параметр *Allow Classic Operations*(Разрешить классические операции) можно включать и отключать.</span><span class="sxs-lookup"><span data-stu-id="1f810-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="1f810-189">Дополнительные сведения об ограничениях и ограничениях см. в разделе toohello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="1f810-189">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="1f810-190">tooenable hello ExpressRoute премиальное дополнение</span><span class="sxs-lookup"><span data-stu-id="1f810-190">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="1f810-191">Премиальное дополнение hello ExpressRoute можно включить для вашей существующей цепи с помощью hello, следующий фрагмент команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1f810-191">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="1f810-192">цепь Hello получают hello ExpressRoute premium дополнительные возможности.</span><span class="sxs-lookup"><span data-stu-id="1f810-192">hello circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="1f810-193">Мы начнем выставления счетов для hello premium дополнительные возможности, как только команда hello успешно запущена.</span><span class="sxs-lookup"><span data-stu-id="1f810-193">We will begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="1f810-194">toodisable hello ExpressRoute премиальное дополнение</span><span class="sxs-lookup"><span data-stu-id="1f810-194">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1f810-195">Эта операция может завершиться ошибкой, если вы используете ресурсы, которые больше, чем то, что разрешено для стандартной схемы hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-195">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="1f810-196">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1f810-196">Note hello following:</span></span>

* <span data-ttu-id="1f810-197">Прежде чем понизить из premium toostandard, необходимо убедиться, hello количество виртуальных сетей, которые связаны toohello канала — меньше 10.</span><span class="sxs-lookup"><span data-stu-id="1f810-197">Before you downgrade from premium toostandard, you must ensure that hello number of virtual networks that are linked toohello circuit is less than 10.</span></span> <span data-ttu-id="1f810-198">Если этого не сделать, запрос на обновление завершится ошибкой и мы будем выставлять вам счета по тарифам ценовой категории "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1f810-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="1f810-199">Все связи с виртуальными сетями в других геополитических регионах необходимо разорвать.</span><span class="sxs-lookup"><span data-stu-id="1f810-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="1f810-200">Если этого не сделать, запрос на обновление завершится ошибкой и мы будем выставлять вам счета по тарифам ценовой категории "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1f810-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="1f810-201">Для частного пиринга таблица маршрутов должна содержать менее 4000 маршрутов.</span><span class="sxs-lookup"><span data-stu-id="1f810-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="1f810-202">Если размер таблицы маршрутов больше 4000 маршрутов, сеанс BGP hello удаляется и не будет снова включено, пока hello число префиксов, объявленных становится меньше 4 000.</span><span class="sxs-lookup"><span data-stu-id="1f810-202">If your route table size is greater than 4,000 routes, hello BGP session drops and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="1f810-203">Надстройка premium hello ExpressRoute для существующей цепи hello можно отключить с помощью hello, выполнив командлет PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1f810-203">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="1f810-204">пропускная способность контура tooupdate hello ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1f810-204">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="1f810-205">Поддерживаемые полосы пропускания для поставщика, проверьте hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="1f810-205">For supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="1f810-206">Можно выбрать любой большего размера, чем размер hello вашей существующей цепи.</span><span class="sxs-lookup"><span data-stu-id="1f810-206">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f810-207">Канал ExpressRoute toorecreate hello возможно, если имеется существующий порт hello недостаточной мощности.</span><span class="sxs-lookup"><span data-stu-id="1f810-207">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="1f810-208">Обновление схемы hello невозможно, если доступна без дополнительной емкости в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="1f810-208">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="1f810-209">Нельзя уменьшить hello пропускной способности канала ExpressRoute без прерывания.</span><span class="sxs-lookup"><span data-stu-id="1f810-209">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="1f810-210">Понижение уровня полосы пропускания необходимо канал ExpressRoute toodeprovision hello и повторной инициализации новый канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1f810-210">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="1f810-211">После определения размера необходимо, используйте следующие команды tooresize hello ваш канал:</span><span class="sxs-lookup"><span data-stu-id="1f810-211">After you decide what size you need, use hello following command tooresize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="1f810-212">Ваш канал будет изменяться размер на стороне Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-212">Your circuit will be sized up on hello Microsoft side.</span></span> <span data-ttu-id="1f810-213">Затем необходимо обратиться к настройки подключения поставщика tooupdate на своей стороне toomatch это изменение.</span><span class="sxs-lookup"><span data-stu-id="1f810-213">Then you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="1f810-214">После внесения этого уведомления, мы начнем выставления счетов за hello обновить параметр пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="1f810-214">After you make this notification, we will begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="1f810-215">hello toomove SKU из отслеживаемых toounlimited</span><span class="sxs-lookup"><span data-stu-id="1f810-215">toomove hello SKU from metered toounlimited</span></span>
<span data-ttu-id="1f810-216">Hello SKU канал ExpressRoute можно изменить с помощью hello, следующий фрагмент команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1f810-216">You can change hello SKU of an ExpressRoute circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="1f810-217">Классический toohello toocontrol доступа и диспетчер ресурсов среды</span><span class="sxs-lookup"><span data-stu-id="1f810-217">toocontrol access toohello classic and Resource Manager environments</span></span>
<span data-ttu-id="1f810-218">Ознакомьтесь с инструкциями hello в [каналы ExpressRoute переместить из модели развертывания диспетчера ресурсов hello классический toohello](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1f810-218">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="1f810-219">Отзыв и удаление канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1f810-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="1f810-220">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1f810-220">Note hello following:</span></span>

* <span data-ttu-id="1f810-221">Необходимо удалить связь всех виртуальных сетей с каналом expressroute hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-221">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="1f810-222">Если операция завершается неудачно, убедитесь, что цепь toohello связанные toosee, если все виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="1f810-222">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="1f810-223">Если состояние подготовки службы поставщика hello ExpressRoute канала **Provisioning** или **инициализировано** необходимо работать с ваш канал hello toodeprovision поставщика службы с их стороны.</span><span class="sxs-lookup"><span data-stu-id="1f810-223">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="1f810-224">Она будет продолжать tooreserve ресурсы и выставлять вам счет на поставщика услуг hello завершения списания цепи hello и уведомляет нас.</span><span class="sxs-lookup"><span data-stu-id="1f810-224">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="1f810-225">Если поставщик услуг hello отозваны hello канала (состояние подготовки поставщика услуг hello задано слишком**не инициализировано**) можно удалить цепь hello.</span><span class="sxs-lookup"><span data-stu-id="1f810-225">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="1f810-226">Это приведет к остановке выставления счетов для схемы hello</span><span class="sxs-lookup"><span data-stu-id="1f810-226">This will stop billing for hello circuit</span></span>

<span data-ttu-id="1f810-227">Ваш канал ExpressRoute можно удалить, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="1f810-227">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="1f810-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f810-228">Next steps</span></span>

<span data-ttu-id="1f810-229">После создания ваш канал, убедитесь, что hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1f810-229">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="1f810-230">Создание и изменение маршрутизации для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1f810-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="1f810-231">Связать вашей виртуальной сети tooyour канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1f810-231">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
