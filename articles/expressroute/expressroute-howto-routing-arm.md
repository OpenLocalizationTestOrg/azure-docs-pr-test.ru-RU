---
title: "Как tooconfigure маршрутизации (пиринг) для канала ExpressRoute: диспетчера ресурсов: PowerShell: Azure | Документы Microsoft"
description: "В этой статье содержится описание этапов hello для создания и подготовки hello private, public и Microsoft пиринг канал ExpressRoute. В этой статье также рассказывается, как состояние toocheck hello, обновления или удаления пиринги для своего канала."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="d6366-104">Создание и изменение пиринга для канала ExpressRoute с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6366-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="d6366-105">Эта статья поможет вам создавать и управлять ими конфигурации маршрутизации для канала ExpressRoute в модели развертывания диспетчера ресурсов hello, с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6366-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="d6366-106">Можно также проверить состояние hello, update или delete и отзыв пиринги за канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="d6366-107">Если вы хотите toouse toowork другой метод с ваш канал, выберите статью из hello после списка:</span><span class="sxs-lookup"><span data-stu-id="d6366-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6366-108">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d6366-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="d6366-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6366-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="d6366-110">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="d6366-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="d6366-111">Видео — частный пиринг</span><span class="sxs-lookup"><span data-stu-id="d6366-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="d6366-112">Видео — общедоступный пиринг</span><span class="sxs-lookup"><span data-stu-id="d6366-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="d6366-113">Видео — пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d6366-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="d6366-114">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="d6366-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="d6366-115">Предварительные требования для настройки</span><span class="sxs-lookup"><span data-stu-id="d6366-115">Configuration prerequisites</span></span>

* <span data-ttu-id="d6366-116">Вам потребуется hello последнюю версию hello командлеты PowerShell диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d6366-116">You will need hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="d6366-117">Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6366-117">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="d6366-118">Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md) страницы hello [требования к маршрутизации](expressroute-routing.md) страницы и hello [рабочих процессов](expressroute-workflows.md) страницы перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="d6366-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="d6366-119">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="d6366-120">Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-arm.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="d6366-120">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="d6366-121">Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен для вас командлеты hello может toorun toobe в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d6366-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in this article.</span></span>

<span data-ttu-id="d6366-122">Эти инструкции применяются только toocircuits, созданных с помощью предложения службы связи уровня 2 поставщиков услуг.</span><span class="sxs-lookup"><span data-stu-id="d6366-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="d6366-123">Если ваш поставщик услуг подключения предлагает услуги третьего уровня (обычно это IPVPN, например MPLS), то он возьмет на себя настройку маршрутизации и управление ею.</span><span class="sxs-lookup"><span data-stu-id="d6366-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6366-124">Мы сейчас не объявляет пиринги настроен поставщиками услуг через портал управления службами hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-124">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="d6366-125">Такая возможность будет предоставлена позже.</span><span class="sxs-lookup"><span data-stu-id="d6366-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="d6366-126">Перед настройкой пирингов BGP уточните информацию у поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="d6366-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="d6366-127">Для каждого канала ExpressRoute можно настроить один, два или три пиринга (частный пиринг Azure, общедоступный пиринг Azure и пиринг Microsoft).</span><span class="sxs-lookup"><span data-stu-id="d6366-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="d6366-128">Пиринги можно настраивать в любом порядке,</span><span class="sxs-lookup"><span data-stu-id="d6366-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="d6366-129">Тем не менее необходимо выполнить настройку hello из каждого из них пиринга одновременно.</span><span class="sxs-lookup"><span data-stu-id="d6366-129">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="d6366-130">Частный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="d6366-130">Azure private peering</span></span>

<span data-ttu-id="d6366-131">Этот раздел поможет вам создать, получить, обновление и удаление hello Azure закрытая конфигурация пиринга канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-131">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="d6366-132">toocreate открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d6366-132">toocreate Azure private peering</span></span>

1. <span data-ttu-id="d6366-133">Импортируйте модуль PowerShell hello для ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-133">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="d6366-134">Необходимо установить установщик последнюю PowerShell hello из [коллекции PowerShell](http://www.powershellgallery.com/) и импортируйте модули диспетчера ресурсов Azure hello в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-134">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="d6366-135">Вам потребуется toorun PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="d6366-135">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="d6366-136">Импортируйте все модули AzureRM.* hello внутри hello известный диапазон версию семантики.</span><span class="sxs-lookup"><span data-stu-id="d6366-136">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="d6366-137">Можно импортировать также просто выберите модуль внутри hello известный диапазон версию семантики.</span><span class="sxs-lookup"><span data-stu-id="d6366-137">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="d6366-138">Войдите в учетную запись tooyour.</span><span class="sxs-lookup"><span data-stu-id="d6366-138">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="d6366-139">Выберите подписку hello требуется toocreate канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-139">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="d6366-140">Создайте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="d6366-141">Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-arm.md) и их подготовки с помощью поставщика услуг подключения hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-141">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="d6366-142">Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас.</span><span class="sxs-lookup"><span data-stu-id="d6366-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="d6366-143">В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-143">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="d6366-144">Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="d6366-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="d6366-145">Убедитесь, что подготовлены, а также включить toomake цепь ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-145">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="d6366-146">Используйте следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-146">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="d6366-147">Hello ответ — аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="d6366-147">hello response is similar toohello following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="d6366-148">Настройка открытого пиринга Azure для hello схемы.</span><span class="sxs-lookup"><span data-stu-id="d6366-148">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="d6366-149">Убедитесь, что hello следующих элементов, прежде чем продолжить hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="d6366-149">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="d6366-150">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-150">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="d6366-151">подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="d6366-151">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="d6366-152">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-152">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="d6366-153">подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="d6366-153">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="d6366-154">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="d6366-154">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="d6366-155">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="d6366-155">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="d6366-156">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="d6366-156">AS number for peering.</span></span> <span data-ttu-id="d6366-157">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="d6366-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="d6366-158">Для этого пиринга можно использовать частный номер AS.</span><span class="sxs-lookup"><span data-stu-id="d6366-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="d6366-159">Не используйте номер 65515.</span><span class="sxs-lookup"><span data-stu-id="d6366-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="d6366-160">**Необязательно —** хэш MD5 при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="d6366-160">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="d6366-161">Используйте следующий пример tooconfigure Azure закрытого пиринга для своего канала hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-161">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="d6366-162">При выборе toouse хэш MD5, используйте следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="d6366-162">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="d6366-163">Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.</span><span class="sxs-lookup"><span data-stu-id="d6366-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="d6366-164">tooview Azure закрытого пиринга подробные сведения</span><span class="sxs-lookup"><span data-stu-id="d6366-164">tooview Azure private peering details</span></span>

<span data-ttu-id="d6366-165">Сведения о конфигурации можно получить с помощью hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="d6366-165">You can get configuration details by using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="d6366-166">tooupdate конфигурации закрытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d6366-166">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="d6366-167">Вы можете обновить любая часть конфигурации hello, используя следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-167">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="d6366-168">В этом примере выполняется обновление hello VLAN ID канала hello из 100 too500.</span><span class="sxs-lookup"><span data-stu-id="d6366-168">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="d6366-169">toodelete открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d6366-169">toodelete Azure private peering</span></span>

<span data-ttu-id="d6366-170">Пиринг конфигурации можно удалить, выполнив следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-170">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="d6366-171">Необходимо убедиться, что все виртуальные сети будут отключены от hello канал ExpressRoute перед запуском этого примера.</span><span class="sxs-lookup"><span data-stu-id="d6366-171">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="d6366-172">Общедоступный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="d6366-172">Azure public peering</span></span>

<span data-ttu-id="d6366-173">Этот раздел поможет вам создать, получить, обновление и удаление hello Azure открытая конфигурация пиринга канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-173">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="d6366-174">toocreate частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d6366-174">toocreate Azure public peering</span></span>

1. <span data-ttu-id="d6366-175">Импортируйте модуль PowerShell hello для ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-175">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="d6366-176">Необходимо установить установщик последнюю PowerShell hello из [коллекции PowerShell](http://www.powershellgallery.com/) и импортируйте модули диспетчера ресурсов Azure hello в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-176">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="d6366-177">Вам потребуется toorun PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="d6366-177">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="d6366-178">Импортируйте все модули AzureRM.* hello внутри hello известный диапазон версию семантики.</span><span class="sxs-lookup"><span data-stu-id="d6366-178">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="d6366-179">Можно импортировать также просто выберите модуль внутри hello известный диапазон версию семантики.</span><span class="sxs-lookup"><span data-stu-id="d6366-179">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="d6366-180">Войдите в учетную запись tooyour.</span><span class="sxs-lookup"><span data-stu-id="d6366-180">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="d6366-181">Выберите подписку hello требуется toocreate канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-181">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="d6366-182">Создайте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="d6366-183">Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-arm.md) и их подготовки с помощью поставщика услуг подключения hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="d6366-184">Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас.</span><span class="sxs-lookup"><span data-stu-id="d6366-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="d6366-185">В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="d6366-186">Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="d6366-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="d6366-187">Проверьте hello tooensure цепь ExpressRoute подготовленный и также включена.</span><span class="sxs-lookup"><span data-stu-id="d6366-187">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="d6366-188">Используйте следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-188">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="d6366-189">Hello ответ — аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="d6366-189">hello response is similar toohello following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="d6366-190">Настройка открытого пиринга Azure для hello схемы.</span><span class="sxs-lookup"><span data-stu-id="d6366-190">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="d6366-191">Убедитесь, что следующие сведения, прежде чем продолжить дальнейшей hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-191">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="d6366-192">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-192">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="d6366-193">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="d6366-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="d6366-194">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-194">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="d6366-195">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="d6366-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="d6366-196">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="d6366-196">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="d6366-197">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="d6366-197">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="d6366-198">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="d6366-198">AS number for peering.</span></span> <span data-ttu-id="d6366-199">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="d6366-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="d6366-200">**Необязательно —** хэш MD5 при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="d6366-200">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="d6366-201">Запустите следующий пример tooconfigure Azure открытый пиринг для своего канала hello</span><span class="sxs-lookup"><span data-stu-id="d6366-201">Run hello following example tooconfigure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="d6366-202">При выборе toouse хэш MD5, используйте следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="d6366-202">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="d6366-203">Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.</span><span class="sxs-lookup"><span data-stu-id="d6366-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="d6366-204">tooview открытый пиринг сведения о Azure</span><span class="sxs-lookup"><span data-stu-id="d6366-204">tooview Azure public peering details</span></span>

<span data-ttu-id="d6366-205">Можно получить сведения о конфигурации, с помощью hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="d6366-205">You can get configuration details using hello following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="d6366-206">tooupdate конфигурации открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d6366-206">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="d6366-207">Вы можете обновить любая часть конфигурации hello, используя следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-207">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="d6366-208">В этом примере выполняется обновление hello VLAN ID канала hello из 200 too600.</span><span class="sxs-lookup"><span data-stu-id="d6366-208">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="d6366-209">toodelete частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d6366-209">toodelete Azure public peering</span></span>

<span data-ttu-id="d6366-210">Пиринг конфигурации можно удалить, выполнив следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-210">You can remove your peering configuration by running hello following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="d6366-211">Пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d6366-211">Microsoft peering</span></span>

<span data-ttu-id="d6366-212">Этот раздел поможет вам создать, получить, обновление и удаление пиринга конфигурации Microsoft hello за канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-212">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6366-213">Microsoft пиринг ExpressRoute каналов, которые были настроены предыдущих tooAugust 1, 2017 г. будет иметь все службы префиксов, объявленных через пиринг Майкрософт hello, даже если не определены фильтры маршрутов.</span><span class="sxs-lookup"><span data-stu-id="d6366-213">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="d6366-214">Пиринг каналы ExpressRoute, настроенных в течение или после 1 августа 2017 г. Корпорация Майкрософт не будет иметь префиксы объявленных пока фильтр не будет подключено toohello канала.</span><span class="sxs-lookup"><span data-stu-id="d6366-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="d6366-215">Дополнительные сведения см. в руководстве по [настройке фильтра маршрута для пиринга Майкрософт](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d6366-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="d6366-216">toocreate пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d6366-216">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="d6366-217">Импортируйте модуль PowerShell hello для ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-217">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="d6366-218">Необходимо установить установщик последнюю PowerShell hello из [коллекции PowerShell](http://www.powershellgallery.com/) и импортируйте модули диспетчера ресурсов Azure hello в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-218">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="d6366-219">Вам потребуется toorun PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="d6366-219">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="d6366-220">Импортируйте все модули AzureRM.* hello внутри hello известный диапазон версию семантики.</span><span class="sxs-lookup"><span data-stu-id="d6366-220">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="d6366-221">Можно импортировать также просто выберите модуль внутри hello известный диапазон версию семантики.</span><span class="sxs-lookup"><span data-stu-id="d6366-221">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="d6366-222">Войдите в учетную запись tooyour.</span><span class="sxs-lookup"><span data-stu-id="d6366-222">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="d6366-223">Выберите подписку hello требуется toocreate канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-223">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="d6366-224">Создайте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d6366-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="d6366-225">Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-arm.md) и их подготовки с помощью поставщика услуг подключения hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-225">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="d6366-226">Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас.</span><span class="sxs-lookup"><span data-stu-id="d6366-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="d6366-227">В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-227">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="d6366-228">Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="d6366-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="d6366-229">Убедитесь, что подготовлены, а также включить toomake цепь ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-229">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="d6366-230">Используйте следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-230">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="d6366-231">Hello ответ — аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="d6366-231">hello response is similar toohello following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="d6366-232">Настройка Microsoft пиринг для цепи hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-232">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="d6366-233">Убедитесь, что hello следующую информацию, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="d6366-233">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="d6366-234">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-234">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="d6366-235">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="d6366-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="d6366-236">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-236">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="d6366-237">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="d6366-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="d6366-238">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="d6366-238">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="d6366-239">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="d6366-239">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="d6366-240">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="d6366-240">AS number for peering.</span></span> <span data-ttu-id="d6366-241">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="d6366-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="d6366-242">Объявленные префиксы: необходимо предоставить список всех префиксов планирование tooadvertise сеансом BGP hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-242">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="d6366-243">Допускаются только общедоступные префиксы IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="d6366-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="d6366-244">Если планируется toosend набор префиксов, вы можете отправить список с разделителями запятыми.</span><span class="sxs-lookup"><span data-stu-id="d6366-244">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="d6366-245">Эти префиксы должны быть tooyou, зарегистрированные в RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="d6366-245">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="d6366-246">**Необязательно —** клиента ASN: если префиксы рекламы, не зарегистрированный toohello пиринг как число, можно указать hello в качестве номера toowhich они зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="d6366-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="d6366-247">Имя реестра маршрутизации: Можно указать hello RIR / IRR, для какой hello, а число и префиксы зарегистрирована.</span><span class="sxs-lookup"><span data-stu-id="d6366-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="d6366-248">**Необязательно —** хэш MD5 при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="d6366-248">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="d6366-249">Используйте следующие пиринг Майкрософт пример tooconfigure для своего канала hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-249">Use hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="d6366-250">данные пиринга tooget Microsoft</span><span class="sxs-lookup"><span data-stu-id="d6366-250">tooget Microsoft peering details</span></span>

<span data-ttu-id="d6366-251">Можно получить сведения о конфигурации, используя следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="d6366-251">You can get configuration details using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="d6366-252">Конфигурация пиринга Майкрософт tooupdate</span><span class="sxs-lookup"><span data-stu-id="d6366-252">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="d6366-253">Можно обновить любая часть конфигурации hello, используя следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-253">You can update any part of hello configuration using hello following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="d6366-254">toodelete пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d6366-254">toodelete Microsoft peering</span></span>

<span data-ttu-id="d6366-255">Пиринг конфигурации можно удалить, выполнив следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="d6366-255">You can remove your peering configuration by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="d6366-256">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6366-256">Next steps</span></span>

<span data-ttu-id="d6366-257">Следующий шаг [связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d6366-257">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="d6366-258">Дополнительную информацию о рабочих процессах ExpressRoute см. в статье [Процедуры ExpressRoute для подготовки каналов и состояний каналов](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="d6366-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="d6366-259">Дополнительную информацию о пиринге канала см. в статье [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="d6366-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="d6366-260">Подробнее о работе с виртуальными сетями см. в статье [Обзор виртуальных сетей](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6366-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
