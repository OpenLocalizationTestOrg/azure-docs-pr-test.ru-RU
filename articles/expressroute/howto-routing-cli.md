---
title: "Как tooconfigure маршрутизации для канала Azure ExpressRoute: CLI | Документы Microsoft"
description: "Эта статья поможет вам создавать и подготавливать hello private, public и Microsoft пиринг канал ExpressRoute. В этой статье также рассказывается, как состояние toocheck hello, обновления или удаления пиринги для своего канала."
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="616cd-104">Создание и изменение маршрутизации для канала ExpressRoute с помощью CLI</span><span class="sxs-lookup"><span data-stu-id="616cd-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="616cd-105">Эта статья поможет вам создавать и управлять ими конфигурации маршрутизации для канала ExpressRoute в модели развертывания диспетчера ресурсов hello, используя интерфейс командной строки.</span><span class="sxs-lookup"><span data-stu-id="616cd-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="616cd-106">Можно также проверить состояние hello, update или delete и отзыв пиринги за канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="616cd-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="616cd-107">Если вы хотите toouse toowork другой метод с ваш канал, выберите статью из hello после списка:</span><span class="sxs-lookup"><span data-stu-id="616cd-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="616cd-108">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="616cd-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="616cd-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="616cd-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="616cd-110">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="616cd-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="616cd-111">Видео — частный пиринг</span><span class="sxs-lookup"><span data-stu-id="616cd-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="616cd-112">Видео — общедоступный пиринг</span><span class="sxs-lookup"><span data-stu-id="616cd-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="616cd-113">Видео — пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="616cd-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="616cd-114">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="616cd-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="616cd-115">Предварительные требования для настройки</span><span class="sxs-lookup"><span data-stu-id="616cd-115">Configuration prerequisites</span></span>

* <span data-ttu-id="616cd-116">Прежде чем начать, установите последнюю версию hello hello команды CLI (2.0 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="616cd-116">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="616cd-117">Сведения об установке hello командах CLI см. в разделе [установить CLI Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="616cd-117">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="616cd-118">Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочего процесса](expressroute-workflows.md) страниц перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="616cd-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="616cd-119">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="616cd-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="616cd-120">Следуйте инструкциям hello слишком[создать канал ExpressRoute](howto-circuit-cli.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="616cd-120">Follow hello instructions too[Create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="616cd-121">Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен для вас команды hello может toorun toobe в этой статье.</span><span class="sxs-lookup"><span data-stu-id="616cd-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello commands in this article.</span></span>

<span data-ttu-id="616cd-122">Эти инструкции применяются только toocircuits, созданных с помощью предложения службы связи уровня 2 поставщиков услуг.</span><span class="sxs-lookup"><span data-stu-id="616cd-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="616cd-123">Если ваш поставщик услуг подключения предлагает услуги третьего уровня (обычно это IPVPN, например MPLS), то он возьмет на себя настройку маршрутизации и управление ею.</span><span class="sxs-lookup"><span data-stu-id="616cd-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="616cd-124">Для каждого канала ExpressRoute можно настроить один, два или все три пиринга (частный пиринг Azure, общедоступный пиринг Azure и пиринг Microsoft).</span><span class="sxs-lookup"><span data-stu-id="616cd-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="616cd-125">Пиринги можно настраивать в любом порядке,</span><span class="sxs-lookup"><span data-stu-id="616cd-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="616cd-126">Тем не менее необходимо выполнить настройку hello из каждого из них пиринга одновременно.</span><span class="sxs-lookup"><span data-stu-id="616cd-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="616cd-127">Частный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="616cd-127">Azure private peering</span></span>

<span data-ttu-id="616cd-128">Этот раздел поможет вам создать, получить, обновление и удаление hello Azure закрытая конфигурация пиринга канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="616cd-128">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="616cd-129">toocreate открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="616cd-129">toocreate Azure private peering</span></span>

1. <span data-ttu-id="616cd-130">Установите последнюю версию hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="616cd-130">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="616cd-131">Необходимо использовать последнюю версию hello hello Azure интерфейс командной строки (CLI). * hello проверки [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="616cd-131">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="616cd-132">Выберите подписку hello требуется канал ExpressRoute toocreate</span><span class="sxs-lookup"><span data-stu-id="616cd-132">Select hello subscription you want toocreate ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="616cd-133">Создайте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="616cd-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="616cd-134">Следуйте инструкциям toocreate hello [канал ExpressRoute](howto-circuit-cli.md) и их подготовки с помощью поставщика услуг подключения hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-134">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="616cd-135">Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас.</span><span class="sxs-lookup"><span data-stu-id="616cd-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="616cd-136">В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-136">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="616cd-137">Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="616cd-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="616cd-138">Убедитесь, что подготовлены, а также включить toomake цепь ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-138">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="616cd-139">Используйте следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-139">Use hello following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="616cd-140">Hello ответ — аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="616cd-140">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="616cd-141">Настройка открытого пиринга Azure для hello схемы.</span><span class="sxs-lookup"><span data-stu-id="616cd-141">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="616cd-142">Убедитесь, что hello следующих элементов, прежде чем продолжить hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="616cd-142">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="616cd-143">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-143">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="616cd-144">подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="616cd-144">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="616cd-145">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-145">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="616cd-146">подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="616cd-146">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="616cd-147">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="616cd-147">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="616cd-148">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="616cd-148">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="616cd-149">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="616cd-149">AS number for peering.</span></span> <span data-ttu-id="616cd-150">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="616cd-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="616cd-151">Для этого пиринга можно использовать частный номер AS.</span><span class="sxs-lookup"><span data-stu-id="616cd-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="616cd-152">Не используйте номер 65515.</span><span class="sxs-lookup"><span data-stu-id="616cd-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="616cd-153">**Необязательно —** хэш MD5 при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="616cd-153">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="616cd-154">Используйте следующий пример tooconfigure Azure закрытого пиринга для своего канала hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-154">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="616cd-155">При выборе toouse хэш MD5, используйте следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="616cd-155">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="616cd-156">Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.</span><span class="sxs-lookup"><span data-stu-id="616cd-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="616cd-157">tooview Azure закрытого пиринга подробные сведения</span><span class="sxs-lookup"><span data-stu-id="616cd-157">tooview Azure private peering details</span></span>

<span data-ttu-id="616cd-158">Сведения о конфигурации можно получить с помощью hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="616cd-158">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="616cd-159">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="616cd-159">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="616cd-160">tooupdate конфигурации закрытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="616cd-160">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="616cd-161">Вы можете обновить любая часть конфигурации hello, используя следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-161">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="616cd-162">В этом примере выполняется обновление hello VLAN ID канала hello из 100 too500.</span><span class="sxs-lookup"><span data-stu-id="616cd-162">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="616cd-163">toodelete открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="616cd-163">toodelete Azure private peering</span></span>

<span data-ttu-id="616cd-164">Пиринг конфигурации можно удалить, выполнив следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-164">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="616cd-165">Необходимо убедиться, что все виртуальные сети будут отключены от hello канал ExpressRoute перед запуском этого примера.</span><span class="sxs-lookup"><span data-stu-id="616cd-165">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="616cd-166">Общедоступный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="616cd-166">Azure public peering</span></span>

<span data-ttu-id="616cd-167">Этот раздел поможет вам создать, получить, обновление и удаление hello Azure открытая конфигурация пиринга канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="616cd-167">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="616cd-168">toocreate частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="616cd-168">toocreate Azure public peering</span></span>

1. <span data-ttu-id="616cd-169">Установите последнюю версию hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="616cd-169">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="616cd-170">Необходимо использовать последнюю версию hello hello Azure интерфейс командной строки (CLI). * hello проверки [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="616cd-170">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="616cd-171">Выберите подписку hello, для которого требуется toocreate канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="616cd-171">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="616cd-172">Создайте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="616cd-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="616cd-173">Следуйте инструкциям toocreate hello [канал ExpressRoute](howto-circuit-cli.md) и их подготовки с помощью поставщика услуг подключения hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-173">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="616cd-174">Если ваш поставщик услуг подключения оказывает услуги третьего уровня, попросите его включить для вас частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="616cd-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="616cd-175">В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-175">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="616cd-176">Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="616cd-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="616cd-177">Проверьте hello tooensure цепь ExpressRoute подготовленный и также включена.</span><span class="sxs-lookup"><span data-stu-id="616cd-177">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="616cd-178">Используйте следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-178">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="616cd-179">Hello ответ — аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="616cd-179">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="616cd-180">Настройка открытого пиринга Azure для hello схемы.</span><span class="sxs-lookup"><span data-stu-id="616cd-180">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="616cd-181">Убедитесь, что следующие сведения, прежде чем продолжить дальнейшей hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-181">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="616cd-182">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-182">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="616cd-183">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="616cd-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="616cd-184">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-184">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="616cd-185">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="616cd-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="616cd-186">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="616cd-186">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="616cd-187">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="616cd-187">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="616cd-188">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="616cd-188">AS number for peering.</span></span> <span data-ttu-id="616cd-189">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="616cd-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="616cd-190">**Необязательно —** хэш MD5 при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="616cd-190">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="616cd-191">Выполните следующий пример tooconfigure Azure открытый пиринг для своего канала hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-191">Run hello following example tooconfigure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="616cd-192">При выборе toouse хэш MD5, используйте следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="616cd-192">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="616cd-193">Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.</span><span class="sxs-lookup"><span data-stu-id="616cd-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="616cd-194">tooview открытый пиринг сведения о Azure</span><span class="sxs-lookup"><span data-stu-id="616cd-194">tooview Azure public peering details</span></span>

<span data-ttu-id="616cd-195">Можно получить сведения о конфигурации, используя следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="616cd-195">You can get configuration details using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="616cd-196">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="616cd-196">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="616cd-197">tooupdate конфигурации открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="616cd-197">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="616cd-198">Вы можете обновить любая часть конфигурации hello, используя следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-198">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="616cd-199">В этом примере выполняется обновление hello VLAN ID канала hello из 200 too600.</span><span class="sxs-lookup"><span data-stu-id="616cd-199">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="616cd-200">toodelete частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="616cd-200">toodelete Azure public peering</span></span>

<span data-ttu-id="616cd-201">Пиринг конфигурации можно удалить, выполнив следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-201">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="616cd-202">Пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="616cd-202">Microsoft peering</span></span>

<span data-ttu-id="616cd-203">Этот раздел поможет вам создать, получить, обновление и удаление пиринга конфигурации Microsoft hello за канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="616cd-203">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="616cd-204">Microsoft пиринг ExpressRoute каналов, которые были настроены предыдущих tooAugust 1, 2017 г. будет иметь все службы префиксов, объявленных через пиринг Майкрософт hello, даже если не определены фильтры маршрутов.</span><span class="sxs-lookup"><span data-stu-id="616cd-204">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="616cd-205">Пиринг каналы ExpressRoute, настроенных в течение или после 1 августа 2017 г. Корпорация Майкрософт не будет иметь префиксы объявленных пока фильтр не будет подключено toohello канала.</span><span class="sxs-lookup"><span data-stu-id="616cd-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="616cd-206">Дополнительные сведения см. в руководстве по [настройке фильтра маршрута для пиринга Майкрософт](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="616cd-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="616cd-207">toocreate пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="616cd-207">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="616cd-208">Установите последнюю версию hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="616cd-208">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="616cd-209">Используйте hello последнюю версию hello Azure интерфейс командной строки (CLI). * hello проверки [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="616cd-209">Use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="616cd-210">Выберите подписку hello, для которого требуется toocreate канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="616cd-210">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="616cd-211">Создайте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="616cd-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="616cd-212">Следуйте инструкциям toocreate hello [канал ExpressRoute](howto-circuit-cli.md) и их подготовки с помощью поставщика услуг подключения hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-212">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="616cd-213">Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас.</span><span class="sxs-lookup"><span data-stu-id="616cd-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="616cd-214">В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-214">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="616cd-215">Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="616cd-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>

3. <span data-ttu-id="616cd-216">Убедитесь, что подготовлены, а также включить toomake цепь ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-216">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="616cd-217">Используйте следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-217">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="616cd-218">Hello ответ — аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="616cd-218">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="616cd-219">Настройка Microsoft пиринг для цепи hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-219">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="616cd-220">Убедитесь, что hello следующую информацию, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="616cd-220">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="616cd-221">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-221">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="616cd-222">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="616cd-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="616cd-223">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-223">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="616cd-224">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="616cd-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="616cd-225">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="616cd-225">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="616cd-226">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="616cd-226">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="616cd-227">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="616cd-227">AS number for peering.</span></span> <span data-ttu-id="616cd-228">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="616cd-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="616cd-229">Объявленные префиксы: необходимо предоставить список всех префиксов планирование tooadvertise сеансом BGP hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-229">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="616cd-230">Допускаются только общедоступные префиксы IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="616cd-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="616cd-231">Если планируется toosend набор префиксов, вы можете отправить список с разделителями запятыми.</span><span class="sxs-lookup"><span data-stu-id="616cd-231">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="616cd-232">Эти префиксы должны быть tooyou, зарегистрированные в RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="616cd-232">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="616cd-233">**Необязательно —** клиента ASN: если префиксы рекламы, не зарегистрированный toohello пиринг как число, можно указать hello в качестве номера toowhich они зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="616cd-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="616cd-234">Имя реестра маршрутизации: Можно указать hello RIR / IRR, для какой hello, а число и префиксы зарегистрирована.</span><span class="sxs-lookup"><span data-stu-id="616cd-234">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="616cd-235">**Необязательно —** хэш MD5 при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="616cd-235">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="616cd-236">Выполните следующие пиринг Майкрософт пример tooconfigure для своего канала hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-236">Run hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="616cd-237">данные пиринга tooget Microsoft</span><span class="sxs-lookup"><span data-stu-id="616cd-237">tooget Microsoft peering details</span></span>

<span data-ttu-id="616cd-238">Сведения о конфигурации можно получить с помощью hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="616cd-238">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="616cd-239">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="616cd-239">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="616cd-240">Конфигурация пиринга Майкрософт tooupdate</span><span class="sxs-lookup"><span data-stu-id="616cd-240">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="616cd-241">Вы можете обновить любая часть конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-241">You can update any part of hello configuration.</span></span> <span data-ttu-id="616cd-242">Hello объявленные префиксы канала hello обновляются с too124.1.0.0/24 123.1.0.0/24 в hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="616cd-242">hello advertised prefixes of hello circuit are being updated from 123.1.0.0/24 too124.1.0.0/24 in hello following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="616cd-243">toodelete пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="616cd-243">toodelete Microsoft peering</span></span>

<span data-ttu-id="616cd-244">Пиринг конфигурации можно удалить, выполнив следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="616cd-244">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="616cd-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="616cd-245">Next steps</span></span>

<span data-ttu-id="616cd-246">Следующий шаг [связывание виртуальной сети tooan канал ExpressRoute](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="616cd-246">Next step, [Link a VNet tooan ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="616cd-247">Дополнительную информацию о рабочих процессах ExpressRoute см. в статье [Процедуры ExpressRoute для подготовки каналов и состояний каналов](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="616cd-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="616cd-248">Дополнительную информацию о пиринге канала см. в статье [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="616cd-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="616cd-249">Подробнее о работе с виртуальными сетями см. в статье [Обзор виртуальных сетей](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="616cd-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>