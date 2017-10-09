---
title: "Создание и изменение канала ExpressRoute Azure с помощью CLI | Документация Майкрософт"
description: "В этой статье описывается toocreate, подготовки, проверьте, обновить, удалить и отзыв канал ExpressRoute с использованием интерфейса CLI."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="495c5-103">Создание и изменение канала ExpressRoute с помощью CLI</span><span class="sxs-lookup"><span data-stu-id="495c5-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="495c5-104">В этой статье описывается, как toocreate канал Azure ExpressRoute с помощью hello интерфейс командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="495c5-104">This article describes how toocreate an Azure ExpressRoute circuit by using hello Command Line Interface (CLI).</span></span> <span data-ttu-id="495c5-105">В этой статье также рассказывается, как состояние toocheck hello, обновить, или удалить и Отмена подготовки схемы.</span><span class="sxs-lookup"><span data-stu-id="495c5-105">This article also shows you how toocheck hello status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="495c5-106">Если требуется toouse toowork другой метод с каналами ExpressRoute hello статьи можно выбрать из hello после списка:</span><span class="sxs-lookup"><span data-stu-id="495c5-106">If you want toouse a different method toowork with ExpressRoute circuits, you can select hello article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="495c5-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="495c5-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="495c5-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="495c5-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="495c5-109">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="495c5-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="495c5-110">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="495c5-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="495c5-111">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="495c5-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="495c5-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="495c5-112">Before you begin</span></span>

* <span data-ttu-id="495c5-113">Прежде чем начать, установите последнюю версию hello hello команды CLI (2.0 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="495c5-113">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="495c5-114">Сведения об установке hello командах CLI см. в разделе [установить CLI Azure 2.0](/cli/azure/install-azure-cli) и [Приступая к работе с Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="495c5-114">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="495c5-115">Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="495c5-115">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="495c5-116">Создание и предоставление канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="495c5-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="495c5-117">1. Войдите в tooyour учетная запись Azure и выберите подписку</span><span class="sxs-lookup"><span data-stu-id="495c5-117">1. Sign in tooyour Azure account and select your subscription</span></span>

<span data-ttu-id="495c5-118">toobegin конфигурацию входа tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="495c5-118">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="495c5-119">Используйте следующие примеры toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-119">Use hello following examples toohelp you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="495c5-120">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-120">Check hello subscriptions for hello account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="495c5-121">Выберите подписку hello, для которого требуется toocreate канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="495c5-121">Select hello subscription for which you want toocreate an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="495c5-122">2. Получить список поддерживаемых поставщиков, расположений и полос пропускания hello</span><span class="sxs-lookup"><span data-stu-id="495c5-122">2. Get hello list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="495c5-123">Прежде чем создавать канал ExpressRoute, необходимо hello список поставщиков поддерживаемых соединений, расположений и полосы пропускания.</span><span class="sxs-lookup"><span data-stu-id="495c5-123">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="495c5-124">Hello CLI команды «az express route списка поставщиков сетевых услуг —» возвращает эту информацию, которая будет использоваться на последующих этапах:</span><span class="sxs-lookup"><span data-stu-id="495c5-124">hello CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="495c5-125">Hello ответ — аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="495c5-125">hello response is similar toohello following example:</span></span>

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

<span data-ttu-id="495c5-126">Проверьте toosee hello ответа, если указана поставщиком соединения.</span><span class="sxs-lookup"><span data-stu-id="495c5-126">Check hello response toosee if your connectivity provider is listed.</span></span> <span data-ttu-id="495c5-127">Запишите hello следующую информацию, который потребуется при создании канала:</span><span class="sxs-lookup"><span data-stu-id="495c5-127">Make a note of hello following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="495c5-128">Имя</span><span class="sxs-lookup"><span data-stu-id="495c5-128">Name</span></span>
* <span data-ttu-id="495c5-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="495c5-129">PeeringLocations</span></span>
* <span data-ttu-id="495c5-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="495c5-130">BandwidthsOffered</span></span>

<span data-ttu-id="495c5-131">Теперь вы готовы toocreate канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="495c5-131">You're now ready toocreate an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="495c5-132">3. Создание канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="495c5-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="495c5-133">Ваш канал ExpressRoute оплачивается с момента hello выдачи ключа службы.</span><span class="sxs-lookup"><span data-stu-id="495c5-133">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="495c5-134">Выполните эту операцию при готовности tooprovision hello цепи hello поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="495c5-134">Perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="495c5-135">Перед созданием канала ExpressRoute необходимо создать группу ресурсов (если вы этого еще не сделали)</span><span class="sxs-lookup"><span data-stu-id="495c5-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="495c5-136">Можно создать группу ресурсов, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="495c5-136">You can create a resource group by running hello following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="495c5-137">Привет, в следующем примере показано, как circuit toocreate ExpressRoute 200 Мбит/с до Equinix в Силиконовой долине.</span><span class="sxs-lookup"><span data-stu-id="495c5-137">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="495c5-138">Если вы используете другой поставщик и другие параметры, подставьте в запрос соответствующие данные.</span><span class="sxs-lookup"><span data-stu-id="495c5-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="495c5-139">Убедитесь, что указан правильный уровень номера SKU hello и семейство номеров SKU:</span><span class="sxs-lookup"><span data-stu-id="495c5-139">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="495c5-140">Уровень SKU определяет, какая надстройка включена — ExpressRoute Standard или ExpressRoute Premium.</span><span class="sxs-lookup"><span data-stu-id="495c5-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="495c5-141">Можно указать «Стандартный» hello tooget стандартном номере SKU или «Premium» hello premium надстройки.</span><span class="sxs-lookup"><span data-stu-id="495c5-141">You can specify 'Standard' tooget hello standard SKU or 'Premium' for hello premium add-on.</span></span>
* <span data-ttu-id="495c5-142">Семейство номеров SKU определяет hello выставления счетов с типом.</span><span class="sxs-lookup"><span data-stu-id="495c5-142">SKU family determines hello billing type.</span></span> <span data-ttu-id="495c5-143">Выберите Metereddata для тарифного плана с оплатой за трафик или Unlimiteddata для безлимитного тарифного плана.</span><span class="sxs-lookup"><span data-stu-id="495c5-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="495c5-144">Можно изменить hello выставления счетов с типом от «Metereddata «too'Unlimiteddata», но не может изменить тип hello из «Unlimiteddata» too'Metereddata».</span><span class="sxs-lookup"><span data-stu-id="495c5-144">You can change hello billing type from 'Metereddata' too'Unlimiteddata', but you can't change hello type from 'Unlimiteddata' too'Metereddata'.</span></span>


<span data-ttu-id="495c5-145">Ваш канал ExpressRoute оплачивается с момента hello выдачи ключа службы.</span><span class="sxs-lookup"><span data-stu-id="495c5-145">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="495c5-146">Следующий пример Hello представляет собой запрос на новый ключ службы:</span><span class="sxs-lookup"><span data-stu-id="495c5-146">hello following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="495c5-147">Hello ответ содержит ключ службы hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-147">hello response contains hello service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="495c5-148">4. Получение списка всех каналов ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="495c5-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="495c5-149">tooget список все каналы ExpressRoute hello, которые были созданы, выполните команду «Список express route сети az» hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-149">tooget a list of all hello ExpressRoute circuits that you created, run hello 'az network express-route list' command.</span></span> <span data-ttu-id="495c5-150">Вы можете получить эти сведения в любое время с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="495c5-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="495c5-151">toolist все каналы сделать hello вызова без параметров.</span><span class="sxs-lookup"><span data-stu-id="495c5-151">toolist all circuits, make hello call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="495c5-152">Ключ службы, перечисленные в hello *ServiceKey* поле ответа hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-152">Your service key is listed in hello *ServiceKey* field of hello response.</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

<span data-ttu-id="495c5-153">Вы можете получить подробное описание всех параметров hello, с помощью hello команды hello "-h" параметра.</span><span class="sxs-lookup"><span data-stu-id="495c5-153">You can get detailed descriptions of all hello parameters by running hello command using hello '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="495c5-154">5. Отправка ключа tooyour подключения hello службы поставщика для подготовки</span><span class="sxs-lookup"><span data-stu-id="495c5-154">5. Send hello service key tooyour connectivity provider for provisioning</span></span>

<span data-ttu-id="495c5-155">«ServiceProviderProvisioningState» предоставляет сведения о текущем состоянии hello подготовки на стороне поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-155">'ServiceProviderProvisioningState' provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="495c5-156">Hello состояния содержит состояние hello hello стороны Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="495c5-156">hello status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="495c5-157">Дополнительные сведения см. в разделе hello [рабочих процессов в статье](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="495c5-157">For more information, see hello [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="495c5-158">При создании нового канала ExpressRoute hello схемы имеет hello следующие состояния:</span><span class="sxs-lookup"><span data-stu-id="495c5-158">When you create a new ExpressRoute circuit, hello circuit is in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="495c5-159">изменения схемы Hello toohello при поставщика услуг подключения hello находится в процессе hello включить его для вас следующие состояния:</span><span class="sxs-lookup"><span data-stu-id="495c5-159">hello circuit changes toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="495c5-160">Для вас toobe может toouse канал ExpressRoute он должен быть в hello следующие состояния:</span><span class="sxs-lookup"><span data-stu-id="495c5-160">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="495c5-161">6. Периодически Проверьте состояние hello и состояние hello ключа канала hello</span><span class="sxs-lookup"><span data-stu-id="495c5-161">6. Periodically check hello status and hello state of hello circuit key</span></span>

<span data-ttu-id="495c5-162">Проверка состояния hello и состояние hello hello ключа канала позволяет узнать, когда поставщик подключит ваш канал.</span><span class="sxs-lookup"><span data-stu-id="495c5-162">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="495c5-163">После настройки канала hello «ServiceProviderProvisioningState» отображается как «Подготовлена», как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="495c5-163">After hello circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in hello following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="495c5-164">Hello ответ — аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="495c5-164">hello response is similar toohello following example:</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="495c5-165">7. Создание конфигурации маршрутизации</span><span class="sxs-lookup"><span data-stu-id="495c5-165">7. Create your routing configuration</span></span>

<span data-ttu-id="495c5-166">Пошаговые инструкции см. в разделе hello [expressroute в конфигурацию маршрутизации](howto-routing-cli.md) статью toocreate и изменения пиринги в цепи.</span><span class="sxs-lookup"><span data-stu-id="495c5-166">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](howto-routing-cli.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="495c5-167">Эти инструкции применяются только toocircuits, созданных с помощью службы поставщиков, предлагающих услуги подключений второго уровня.</span><span class="sxs-lookup"><span data-stu-id="495c5-167">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="495c5-168">Если ваш поставщик услуг подключения предлагает услуги третьего уровня (обычно это IPVPN, например MPLS), то он возьмет на себя настройку маршрутизации и управление ею.</span><span class="sxs-lookup"><span data-stu-id="495c5-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="495c5-169">8. Связывание виртуальной сети tooan канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="495c5-169">8. Link a virtual network tooan ExpressRoute circuit</span></span>

<span data-ttu-id="495c5-170">Затем свяжите виртуальной сети tooyour канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="495c5-170">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="495c5-171">Используйте hello [связывание виртуальной сети цепи tooExpressRoute](howto-linkvnet-cli.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="495c5-171">Use hello [Linking virtual networks tooExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="495c5-172"><a name="modify"></a>Изменение канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="495c5-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="495c5-173">Некоторые свойства канала ExpressRoute можно изменить, не повлияв на подключение.</span><span class="sxs-lookup"><span data-stu-id="495c5-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="495c5-174">Можно внести следующие изменения без простоев hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-174">You can make hello following changes with no downtime:</span></span>

* <span data-ttu-id="495c5-175">Включать и отключать надстройку ExpressRoute "Премиум" для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="495c5-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="495c5-176">Можно увеличить hello пропускной способностью вашего канала ExpressRoute условии, что емкость доступны через порт hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-176">You can increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="495c5-177">Тем не менее понижение уровня полосы пропускания канала hello не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="495c5-177">However, downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="495c5-178">Можно изменить план контроля использования программных продуктов hello с измеряемые данных tooUnlimited данных.</span><span class="sxs-lookup"><span data-stu-id="495c5-178">You can change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="495c5-179">Однако изменение hello измерения план из данных tooMetered данных не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="495c5-179">However, changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="495c5-180">Параметр *Allow Classic Operations*(Разрешить классические операции) можно включать и отключать.</span><span class="sxs-lookup"><span data-stu-id="495c5-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="495c5-181">Дополнительные сведения об ограничениях и ограничениях см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="495c5-181">For more information on limits and limitations, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="495c5-182">tooenable hello ExpressRoute премиальное дополнение</span><span class="sxs-lookup"><span data-stu-id="495c5-182">tooenable hello ExpressRoute premium add-on</span></span>

<span data-ttu-id="495c5-183">Премиальное дополнение hello ExpressRoute можно включить для вашей существующей цепи с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="495c5-183">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="495c5-184">цепь Hello теперь имеет hello ExpressRoute premium дополнительные возможности.</span><span class="sxs-lookup"><span data-stu-id="495c5-184">hello circuit now has hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="495c5-185">Мы начинаем выставления счетов для hello premium дополнительные возможности, как только команда hello успешно запущена.</span><span class="sxs-lookup"><span data-stu-id="495c5-185">We begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="495c5-186">toodisable hello ExpressRoute премиальное дополнение</span><span class="sxs-lookup"><span data-stu-id="495c5-186">toodisable hello ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="495c5-187">Эта операция может завершиться ошибкой, если вы используете ресурсы, которые больше, чем то, что разрешено для стандартной схемы hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-187">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="495c5-188">Перед отключением hello ExpressRoute премиальное дополнение, понять hello следующие условия:</span><span class="sxs-lookup"><span data-stu-id="495c5-188">Before disabling hello ExpressRoute premium add-on, understand hello following criteria:</span></span>

* <span data-ttu-id="495c5-189">Перед понизить из premium toostandard, убедитесь, что имеется менее 10 цепи связанных toohello виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="495c5-189">Before you downgrade from premium toostandard, you must make sure that you have fewer than 10 virtual networks linked toohello circuit.</span></span> <span data-ttu-id="495c5-190">Если у вас их больше 10, запрос на обновление завершится ошибкой и мы будем выставлять вам счета по тарифам ценовой категории "Премиум".</span><span class="sxs-lookup"><span data-stu-id="495c5-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="495c5-191">Все связи с виртуальными сетями в других геополитических регионах необходимо разорвать.</span><span class="sxs-lookup"><span data-stu-id="495c5-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="495c5-192">Если вы не отсоедините все ваши виртуальные сети, запрос обновления завершится ошибкой и мы будем выставлять вам счета по тарифам ценовой категории "Премиум".</span><span class="sxs-lookup"><span data-stu-id="495c5-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="495c5-193">Для частного пиринга таблица маршрутов должна содержать менее 4000 маршрутов.</span><span class="sxs-lookup"><span data-stu-id="495c5-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="495c5-194">Если размер таблицы маршрутов больше 4000 маршрутов, удаляет сеанс BGP hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-194">If your route table size is greater than 4,000 routes, hello BGP session drops.</span></span> <span data-ttu-id="495c5-195">Hello сеанс не будет повторно включать до hello число префиксов, объявленных меньше 4 000.</span><span class="sxs-lookup"><span data-stu-id="495c5-195">hello session won't be reenabled until hello number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="495c5-196">Надстройка premium hello ExpressRoute для существующей цепи hello можно отключить с помощью hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="495c5-196">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="495c5-197">пропускная способность контура tooupdate hello ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="495c5-197">tooupdate hello ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="495c5-198">Параметры пропускной способности hello поддерживается для поставщика, проверьте hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="495c5-198">For hello supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="495c5-199">Можно выбрать любой большего размера, чем размер hello вашей существующей цепи.</span><span class="sxs-lookup"><span data-stu-id="495c5-199">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="495c5-200">Если имеется существующий порт hello недостаточной емкости, имеется канал ExpressRoute toorecreate hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-200">If there is inadequate capacity on hello existing port, you may have toorecreate hello ExpressRoute circuit.</span></span> <span data-ttu-id="495c5-201">Обновление схемы hello невозможно, если доступна без дополнительной емкости в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="495c5-201">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="495c5-202">Нельзя уменьшить hello пропускной способности канала ExpressRoute без прерывания.</span><span class="sxs-lookup"><span data-stu-id="495c5-202">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="495c5-203">Понижение уровня полосы пропускания требует вы toodeprovision hello канал ExpressRoute и повторной инициализации новый канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="495c5-203">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="495c5-204">После принятия решения необходимо использовать ваш канал hello, следующая команда tooresize размер hello:</span><span class="sxs-lookup"><span data-stu-id="495c5-204">After you decide hello size you need, use hello following command tooresize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="495c5-205">Ваш канал подбирается на стороне Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-205">Your circuit is sized up on hello Microsoft side.</span></span> <span data-ttu-id="495c5-206">После этого необходимо обратиться к настройки подключения поставщика tooupdate на своей стороне toomatch это изменение.</span><span class="sxs-lookup"><span data-stu-id="495c5-206">Next, you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="495c5-207">После внесения этого уведомления, мы начинаем выставления счетов за hello обновить параметр пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="495c5-207">After you make this notification, we begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="495c5-208">hello toomove SKU из отслеживаемых toounlimited</span><span class="sxs-lookup"><span data-stu-id="495c5-208">toomove hello SKU from metered toounlimited</span></span>

<span data-ttu-id="495c5-209">Hello SKU канал ExpressRoute можно изменить с помощью hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="495c5-209">You can change hello SKU of an ExpressRoute circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="495c5-210">Классический toohello toocontrol доступа и диспетчер ресурсов среды</span><span class="sxs-lookup"><span data-stu-id="495c5-210">toocontrol access toohello classic and Resource Manager environments</span></span>

<span data-ttu-id="495c5-211">Ознакомьтесь с инструкциями hello в [каналы ExpressRoute переместить из модели развертывания диспетчера ресурсов hello классический toohello](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="495c5-211">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="495c5-212">Отзыв и удаление канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="495c5-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="495c5-213">toodeprovision и удалить канал ExpressRoute убедитесь, что вы понимаете hello следующие условия:</span><span class="sxs-lookup"><span data-stu-id="495c5-213">toodeprovision and delete an ExpressRoute circuit, make sure you understand hello following criteria:</span></span>

* <span data-ttu-id="495c5-214">Необходимо удалить связь всех виртуальных сетей с каналом expressroute hello.</span><span class="sxs-lookup"><span data-stu-id="495c5-214">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="495c5-215">Если операция завершается неудачно, убедитесь, что цепь toohello связанные toosee, если все виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="495c5-215">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="495c5-216">Если состояние подготовки службы поставщика hello ExpressRoute канала **Provisioning** или **инициализировано**, необходимо работать с ваш канал hello toodeprovision поставщика службы с их стороны.</span><span class="sxs-lookup"><span data-stu-id="495c5-216">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="495c5-217">Мы продолжить tooreserve ресурсы и выставлять вам счет на поставщика услуг hello завершения списания цепи hello и уведомляет нас.</span><span class="sxs-lookup"><span data-stu-id="495c5-217">We continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="495c5-218">Hello канала можно удалить, если поставщик услуг hello отозваны hello канала.</span><span class="sxs-lookup"><span data-stu-id="495c5-218">You can delete hello circuit if hello service provider has deprovisioned hello circuit.</span></span> <span data-ttu-id="495c5-219">Если канала отозваны, состояние подготовки поставщика услуг hello устанавливается слишком**не инициализировано**.</span><span class="sxs-lookup"><span data-stu-id="495c5-219">When a circuit is deprovisioned, hello service provider provisioning state is set too**Not provisioned**.</span></span> <span data-ttu-id="495c5-220">Это приостанавливает выставление счетов для hello схемы.</span><span class="sxs-lookup"><span data-stu-id="495c5-220">This stops billing for hello circuit.</span></span>

<span data-ttu-id="495c5-221">Ваш канал ExpressRoute можно удалить, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="495c5-221">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="495c5-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="495c5-222">Next steps</span></span>

<span data-ttu-id="495c5-223">После создания ваш канал, убедитесь, что hello следующие задания:</span><span class="sxs-lookup"><span data-stu-id="495c5-223">After you create your circuit, make sure that you do hello following tasks:</span></span>

* [<span data-ttu-id="495c5-224">Создание и изменение маршрутизации для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="495c5-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="495c5-225">Связать вашей виртуальной сети tooyour канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="495c5-225">Link your virtual network tooyour ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)
