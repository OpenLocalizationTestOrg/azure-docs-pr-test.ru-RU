---
title: "Как tooconfigure маршрутизации (пиринг) для канала ExpressRoute: Azure: классический | Документы Microsoft"
description: "В этой статье содержится описание этапов hello для создания и подготовки hello private, public и Microsoft пиринг канал ExpressRoute. В этой статье также рассказывается, как состояние toocheck hello, обновления или удаления пиринги для своего канала."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="ec61f-104">Создание и изменение пиринга для канала ExpressRoute (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="ec61f-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec61f-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ec61f-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="ec61f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec61f-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="ec61f-107">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="ec61f-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="ec61f-108">Видео — частный пиринг</span><span class="sxs-lookup"><span data-stu-id="ec61f-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ec61f-109">Видео — общедоступный пиринг</span><span class="sxs-lookup"><span data-stu-id="ec61f-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ec61f-110">Видео — пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="ec61f-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ec61f-111">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="ec61f-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="ec61f-112">Данная статья поможет выполнить шаги toocreate hello и управление конфигурацией маршрутизации для канала ExpressRoute с помощью PowerShell и hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ec61f-112">This article walks you through hello steps toocreate and manage routing configuration for an ExpressRoute circuit using PowerShell and hello classic deployment model.</span></span> <span data-ttu-id="ec61f-113">Hello шаги также отображается как toocheck hello состояния, обновление, или удалить и отзыв пиринги за канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ec61f-113">hello steps below will also show you how toocheck hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="ec61f-114">**О моделях развертывания Azure**</span><span class="sxs-lookup"><span data-stu-id="ec61f-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="ec61f-115">Предварительные требования для настройки</span><span class="sxs-lookup"><span data-stu-id="ec61f-115">Configuration prerequisites</span></span>
* <span data-ttu-id="ec61f-116">Вам потребуется hello последнюю версию hello командлеты PowerShell Azure службы управления (SM).</span><span class="sxs-lookup"><span data-stu-id="ec61f-116">You will need hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="ec61f-117">Дополнительные сведения см. в разделе [Приступая к работе с командлетами Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ec61f-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="ec61f-118">Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md) страницы hello [требования к маршрутизации](expressroute-routing.md) страницы и hello [рабочих процессов](expressroute-workflows.md) страницы перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="ec61f-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="ec61f-119">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ec61f-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="ec61f-120">Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-classic.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="ec61f-120">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="ec61f-121">Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен для вас toobe может toorun hello командлетов, описанных ниже.</span><span class="sxs-lookup"><span data-stu-id="ec61f-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec61f-122">Эти инструкции применяются только toocircuits, созданных с помощью предложения службы связи уровня 2 поставщиков услуг.</span><span class="sxs-lookup"><span data-stu-id="ec61f-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="ec61f-123">Если вы работаете с поставщиком, предлагающим услуги третьего уровня (обычно IPVPN, типа MPLS), ваш поставщик услуг подключения выполнит настройку и управление конфигурацией самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="ec61f-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="ec61f-124">Для каждого канала ExpressRoute можно настроить один, два или три пиринга (частный пиринг Azure, общедоступный пиринг Azure и пиринг Microsoft).</span><span class="sxs-lookup"><span data-stu-id="ec61f-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="ec61f-125">Пиринги можно настраивать в любом порядке,</span><span class="sxs-lookup"><span data-stu-id="ec61f-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="ec61f-126">Тем не менее необходимо выполнить настройку hello из каждого из них пиринга одновременно.</span><span class="sxs-lookup"><span data-stu-id="ec61f-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="ec61f-127">Войдите в tooyour учетная запись Azure и выберите подписку</span><span class="sxs-lookup"><span data-stu-id="ec61f-127">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="ec61f-128">Откройте консоль PowerShell с повышенными правами и подключите tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ec61f-128">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="ec61f-129">Используйте следующий пример toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-129">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="ec61f-130">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-130">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="ec61f-131">При наличии нескольких подписок выберите подписку hello, что требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="ec61f-131">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="ec61f-132">Затем используйте следующий командлет tooadd hello tooPowerShell вашей подписки Azure для hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ec61f-132">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="ec61f-133">Частный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="ec61f-133">Azure private peering</span></span>
<span data-ttu-id="ec61f-134">В этом разделе описано, как toocreate, получение, обновление и удаление hello Azure закрытая конфигурация пиринга канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ec61f-134">This section provides instructions on how toocreate, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="ec61f-135">toocreate открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="ec61f-135">toocreate Azure private peering</span></span>
1. <span data-ttu-id="ec61f-136">**Импортируйте модуль PowerShell hello для ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="ec61f-136">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="ec61f-137">Модули Azure и ExpressRoute hello необходимо импортировать в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-137">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="ec61f-138">Выполнения hello следующими командами tooimport hello Azure и ExpressRoute модулей в сеанс PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-138">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="ec61f-139">**Создайте канал ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="ec61f-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="ec61f-140">Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-classic.md) и их подготовки с помощью поставщика услуг подключения hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-140">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="ec61f-141">Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас.</span><span class="sxs-lookup"><span data-stu-id="ec61f-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="ec61f-142">В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-142">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="ec61f-143">Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, выполните приведенные ниже инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span> 
3. <span data-ttu-id="ec61f-144">**Проверьте tooensure цепь ExpressRoute hello, его инициализации.**</span><span class="sxs-lookup"><span data-stu-id="ec61f-144">**Check hello ExpressRoute circuit tooensure it is provisioned.**</span></span>
   
    <span data-ttu-id="ec61f-145">Если hello канал ExpressRoute подготовлены и включены также необходимо отметить toosee.</span><span class="sxs-lookup"><span data-stu-id="ec61f-145">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="ec61f-146">См. ниже пример hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-146">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="ec61f-147">Убедитесь, что hello цепь подготовлена и включен.</span><span class="sxs-lookup"><span data-stu-id="ec61f-147">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="ec61f-148">Если это не так, работаете с вашей tooget поставщика подключения канала требуется toohello состояние и состояние.</span><span class="sxs-lookup"><span data-stu-id="ec61f-148">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="ec61f-149">**Настройка открытого пиринга Azure для hello схемы.**</span><span class="sxs-lookup"><span data-stu-id="ec61f-149">**Configure Azure private peering for hello circuit.**</span></span>
   
    <span data-ttu-id="ec61f-150">Убедитесь, что hello следующих элементов, прежде чем продолжить hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ec61f-150">Make sure that you have hello following items before you proceed with hello next steps:</span></span>
   
   * <span data-ttu-id="ec61f-151">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-151">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="ec61f-152">Она не должна входить в адресное пространство, зарезервированное для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="ec61f-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="ec61f-153">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-153">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="ec61f-154">Она не должна входить в адресное пространство, зарезервированное для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="ec61f-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="ec61f-155">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="ec61f-155">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="ec61f-156">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="ec61f-156">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="ec61f-157">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="ec61f-157">AS number for peering.</span></span> <span data-ttu-id="ec61f-158">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="ec61f-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="ec61f-159">Для этого пиринга можно использовать частный номер AS.</span><span class="sxs-lookup"><span data-stu-id="ec61f-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="ec61f-160">Не используйте номер 65515.</span><span class="sxs-lookup"><span data-stu-id="ec61f-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="ec61f-161">Хэш MD5 при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="ec61f-161">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="ec61f-162">**Это необязательно**.</span><span class="sxs-lookup"><span data-stu-id="ec61f-162">**This is optional**.</span></span>
     
    <span data-ttu-id="ec61f-163">Можно выполнить следующий командлет tooconfigure открытого пиринга Azure для своего канала hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-163">You can run hello following cmdlet tooconfigure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="ec61f-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="ec61f-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="ec61f-165">При выборе toouse хэш MD5, можно использовать командлет hello ниже.</span><span class="sxs-lookup"><span data-stu-id="ec61f-165">You can use hello cmdlet below if you choose toouse an MD5 hash.</span></span>
     
        <span data-ttu-id="ec61f-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="ec61f-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="ec61f-167">Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.</span><span class="sxs-lookup"><span data-stu-id="ec61f-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="ec61f-168">tooview Azure закрытого пиринга подробные сведения</span><span class="sxs-lookup"><span data-stu-id="ec61f-168">tooview Azure private peering details</span></span>
<span data-ttu-id="ec61f-169">Можно получить сведения о конфигурации, с помощью hello, выполнив командлет</span><span class="sxs-lookup"><span data-stu-id="ec61f-169">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="ec61f-170">tooupdate конфигурации закрытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="ec61f-170">tooupdate Azure private peering configuration</span></span>
<span data-ttu-id="ec61f-171">Можно обновить любой части hello конфигурации, с помощью hello, выполнив командлет.</span><span class="sxs-lookup"><span data-stu-id="ec61f-171">You can update any part of hello configuration using hello following cmdlet.</span></span> <span data-ttu-id="ec61f-172">В следующем примере hello hello VLAN ID канала hello обновляется из 100 too500.</span><span class="sxs-lookup"><span data-stu-id="ec61f-172">In hello example below, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="ec61f-173">toodelete открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="ec61f-173">toodelete Azure private peering</span></span>
<span data-ttu-id="ec61f-174">Можно удалить пиринг конфигурацию, выполнив следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-174">You can remove your peering configuration by running hello following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="ec61f-175">Необходимо убедиться, что все виртуальные сети будут отключены от hello канал ExpressRoute перед выполнением этого командлета.</span><span class="sxs-lookup"><span data-stu-id="ec61f-175">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="ec61f-176">Общедоступный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="ec61f-176">Azure public peering</span></span>
<span data-ttu-id="ec61f-177">В этом разделе описано, как toocreate, получение, обновление и удаление hello Azure открытая конфигурация пиринга канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ec61f-177">This section provides instructions on how toocreate, get, update and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="ec61f-178">toocreate частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="ec61f-178">toocreate Azure public peering</span></span>
1. <span data-ttu-id="ec61f-179">**Импортируйте модуль PowerShell hello для ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="ec61f-179">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="ec61f-180">Модули Azure и ExpressRoute hello необходимо импортировать в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-180">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="ec61f-181">Выполнения hello следующими командами tooimport hello Azure и ExpressRoute модулей в сеанс PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-181">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="ec61f-182">**Создание канала ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="ec61f-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="ec61f-183">Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-classic.md) и их подготовки с помощью поставщика услуг подключения hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="ec61f-184">Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure открытый пиринг для вас.</span><span class="sxs-lookup"><span data-stu-id="ec61f-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure public peering for you.</span></span> <span data-ttu-id="ec61f-185">В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="ec61f-186">Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, выполните приведенные ниже инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="ec61f-187">**Проверьте tooensure цепь ExpressRoute, он предоставляется**</span><span class="sxs-lookup"><span data-stu-id="ec61f-187">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="ec61f-188">Если hello канал ExpressRoute подготовлены и включены также необходимо отметить toosee.</span><span class="sxs-lookup"><span data-stu-id="ec61f-188">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="ec61f-189">См. ниже пример hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-189">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="ec61f-190">Убедитесь, что hello цепь подготовлена и включен.</span><span class="sxs-lookup"><span data-stu-id="ec61f-190">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="ec61f-191">Если это не так, работаете с вашей tooget поставщика подключения канала требуется toohello состояние и состояние.</span><span class="sxs-lookup"><span data-stu-id="ec61f-191">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="ec61f-192">**Настройка открытого пиринга Azure для схемы hello**</span><span class="sxs-lookup"><span data-stu-id="ec61f-192">**Configure Azure public peering for hello circuit**</span></span>
   
    <span data-ttu-id="ec61f-193">Убедитесь, что hello следующую информацию, прежде чем продолжить, далее.</span><span class="sxs-lookup"><span data-stu-id="ec61f-193">Ensure that you have hello following information before you proceed further.</span></span>
   
   * <span data-ttu-id="ec61f-194">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-194">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="ec61f-195">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="ec61f-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="ec61f-196">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-196">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="ec61f-197">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="ec61f-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="ec61f-198">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="ec61f-198">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="ec61f-199">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="ec61f-199">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="ec61f-200">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="ec61f-200">AS number for peering.</span></span> <span data-ttu-id="ec61f-201">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="ec61f-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="ec61f-202">Хэш MD5 при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="ec61f-202">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="ec61f-203">**Это необязательно**.</span><span class="sxs-lookup"><span data-stu-id="ec61f-203">**This is optional**.</span></span>
     
    <span data-ttu-id="ec61f-204">Можно выполнить следующий командлет tooconfigure открытого пиринга Azure для своего канала hello</span><span class="sxs-lookup"><span data-stu-id="ec61f-204">You can run hello following cmdlet tooconfigure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="ec61f-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="ec61f-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="ec61f-206">При выборе toouse MD5-хэш можно использовать командлет hello</span><span class="sxs-lookup"><span data-stu-id="ec61f-206">You can use hello cmdlet below if you choose toouse an MD5 hash</span></span>
     
        <span data-ttu-id="ec61f-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="ec61f-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="ec61f-208">Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.</span><span class="sxs-lookup"><span data-stu-id="ec61f-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="ec61f-209">tooview открытый пиринг сведения о Azure</span><span class="sxs-lookup"><span data-stu-id="ec61f-209">tooview Azure public peering details</span></span>
<span data-ttu-id="ec61f-210">Можно получить сведения о конфигурации, с помощью hello, выполнив командлет</span><span class="sxs-lookup"><span data-stu-id="ec61f-210">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="ec61f-211">tooupdate конфигурации открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="ec61f-211">tooupdate Azure public peering configuration</span></span>
<span data-ttu-id="ec61f-212">Можно обновить любой части hello конфигурации, с помощью hello, выполнив командлет</span><span class="sxs-lookup"><span data-stu-id="ec61f-212">You can update any part of hello configuration using hello following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="ec61f-213">Hello VLAN ID канала hello обновляется из 200 too600 в hello в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="ec61f-213">hello VLAN ID of hello circuit is being updated from 200 too600 in hello above example.</span></span>

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="ec61f-214">toodelete частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="ec61f-214">toodelete Azure public peering</span></span>
<span data-ttu-id="ec61f-215">Можно удалить пиринг конфигурацию, выполнив следующий командлет hello</span><span class="sxs-lookup"><span data-stu-id="ec61f-215">You can remove your peering configuration by running hello following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="ec61f-216">Пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="ec61f-216">Microsoft peering</span></span>
<span data-ttu-id="ec61f-217">В этом разделе описано, как toocreate, получения, обновления и удаления конфигурации пиринг Microsoft hello за канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ec61f-217">This section provides instructions on how toocreate, get, update and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="ec61f-218">toocreate пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="ec61f-218">toocreate Microsoft peering</span></span>
1. <span data-ttu-id="ec61f-219">**Импортируйте модуль PowerShell hello для ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="ec61f-219">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="ec61f-220">Модули Azure и ExpressRoute hello необходимо импортировать в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-220">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="ec61f-221">Выполнения hello следующими командами tooimport hello Azure и ExpressRoute модулей в сеанс PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-221">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="ec61f-222">**Создание канала ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="ec61f-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="ec61f-223">Следуйте инструкциям toocreate hello [канал ExpressRoute](expressroute-howto-circuit-classic.md) и их подготовки с помощью поставщика услуг подключения hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-223">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="ec61f-224">Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас.</span><span class="sxs-lookup"><span data-stu-id="ec61f-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="ec61f-225">В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-225">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="ec61f-226">Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, выполните приведенные ниже инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="ec61f-227">**Проверьте tooensure цепь ExpressRoute, он предоставляется**</span><span class="sxs-lookup"><span data-stu-id="ec61f-227">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="ec61f-228">Сначала необходимо проверить toosee, если hello канал ExpressRoute находится в состоянии подготовлена и включен.</span><span class="sxs-lookup"><span data-stu-id="ec61f-228">You must first check toosee if hello ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="ec61f-229">Убедитесь, что hello цепь подготовлена и включен.</span><span class="sxs-lookup"><span data-stu-id="ec61f-229">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="ec61f-230">Если это не так, работаете с вашей tooget поставщика подключения канала требуется toohello состояние и состояние.</span><span class="sxs-lookup"><span data-stu-id="ec61f-230">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="ec61f-231">**Настройка Microsoft пиринг для цепи hello**</span><span class="sxs-lookup"><span data-stu-id="ec61f-231">**Configure Microsoft peering for hello circuit**</span></span>
   
    <span data-ttu-id="ec61f-232">Убедитесь, что hello следующую информацию, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="ec61f-232">Make sure that you have hello following information before you proceed.</span></span>
   
   * <span data-ttu-id="ec61f-233">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-233">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="ec61f-234">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="ec61f-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="ec61f-235">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-235">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="ec61f-236">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="ec61f-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="ec61f-237">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="ec61f-237">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="ec61f-238">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="ec61f-238">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="ec61f-239">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="ec61f-239">AS number for peering.</span></span> <span data-ttu-id="ec61f-240">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="ec61f-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="ec61f-241">Объявленные префиксы: необходимо предоставить список всех префиксов планирование tooadvertise сеансом BGP hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-241">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="ec61f-242">Допускаются только общедоступные префиксы IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ec61f-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="ec61f-243">Если планируется toosend набор префиксов можно отправить список разделенных запятыми.</span><span class="sxs-lookup"><span data-stu-id="ec61f-243">You can send a comma separated list if you plan toosend a set of prefixes.</span></span> <span data-ttu-id="ec61f-244">Эти префиксы должны быть tooyou, зарегистрированные в RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="ec61f-244">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
   * <span data-ttu-id="ec61f-245">Клиент ASN: Если вы размещаете рекламу, не зарегистрированный toohello пиринг как число префиксов, можно указать hello как число toowhich их регистрации.</span><span class="sxs-lookup"><span data-stu-id="ec61f-245">Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span> <span data-ttu-id="ec61f-246">**Это необязательно**.</span><span class="sxs-lookup"><span data-stu-id="ec61f-246">**This is optional**.</span></span>
   * <span data-ttu-id="ec61f-247">Имя реестра маршрутизации: Можно указать hello RIR / IRR, для какой hello, а число и префиксы зарегистрирована.</span><span class="sxs-lookup"><span data-stu-id="ec61f-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="ec61f-248">Хэш MD5, при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="ec61f-248">An MD5 hash, if you choose toouse one.</span></span> <span data-ttu-id="ec61f-249">**Это необязательно.**</span><span class="sxs-lookup"><span data-stu-id="ec61f-249">**This is optional.**</span></span>
     
    <span data-ttu-id="ec61f-250">Можно выполнить следующий командлет tooconfigure Microsoft pering для своего канала hello</span><span class="sxs-lookup"><span data-stu-id="ec61f-250">You can run hello following cmdlet tooconfigure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="ec61f-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="ec61f-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="ec61f-252">данные пиринга tooview Microsoft</span><span class="sxs-lookup"><span data-stu-id="ec61f-252">tooview Microsoft peering details</span></span>
<span data-ttu-id="ec61f-253">Можно получить сведения о конфигурации, используя следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-253">You can get configuration details using hello following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="ec61f-254">Конфигурация пиринга Майкрософт tooupdate</span><span class="sxs-lookup"><span data-stu-id="ec61f-254">tooupdate Microsoft peering configuration</span></span>
<span data-ttu-id="ec61f-255">Можно обновить любой части hello конфигурации, с помощью hello, выполнив командлет.</span><span class="sxs-lookup"><span data-stu-id="ec61f-255">You can update any part of hello configuration using hello following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="ec61f-256">toodelete пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="ec61f-256">toodelete Microsoft peering</span></span>
<span data-ttu-id="ec61f-257">Можно удалить пиринг конфигурацию, выполнив следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="ec61f-257">You can remove your peering configuration by running hello following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="ec61f-258">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec61f-258">Next steps</span></span>
<span data-ttu-id="ec61f-259">Далее, [связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="ec61f-259">Next, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="ec61f-260">Дополнительные сведения о рабочих процессах см. в разделе [Рабочие процессы ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="ec61f-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="ec61f-261">Дополнительную информацию о пиринге канала см. в статье [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="ec61f-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

