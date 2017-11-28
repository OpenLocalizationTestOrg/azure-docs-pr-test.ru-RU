---
title: "Проверка подключения. Руководство по устранению неполадок Azure ExpressRoute | Документация Майкрософт"
description: "Эта страница содержит инструкции Устранение неполадок и проверка подключения tooend end из канала ExpressRoute."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="ef635-103">Проверка подключения ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ef635-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="ef635-104">ExpressRoute, которая расширяет локальную сеть в облако Microsoft hello через подключение к частной, можно добиться с помощью поставщика услуг подключения, включает в себя следующие три различных сетевых зоны hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-104">ExpressRoute, which extends an on-premises network into hello Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves hello following three distinct network zones:</span></span>

-   <span data-ttu-id="ef635-105">клиентскую сеть;</span><span class="sxs-lookup"><span data-stu-id="ef635-105">Customer Network</span></span>
-   <span data-ttu-id="ef635-106">сеть поставщика;</span><span class="sxs-lookup"><span data-stu-id="ef635-106">Provider Network</span></span>
-   <span data-ttu-id="ef635-107">центр обработки данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ef635-107">Microsoft Datacenter</span></span>

<span data-ttu-id="ef635-108">Hello цель данного документа — tooidentify пользователя toohelp где (или даже в том случае, если) существует проблема с подключением и в пределах зоны, тем самым tooseek помощь в соответствующую группу tooresolve hello проблему.</span><span class="sxs-lookup"><span data-stu-id="ef635-108">hello purpose of this document is toohelp user tooidentify where (or even if) a connectivity issue exists and within which zone, thereby tooseek help from appropriate team tooresolve hello issue.</span></span> <span data-ttu-id="ef635-109">Если службу технической поддержки Майкрософт необходимые tooresolve проблему, откройте запрос в службу поддержки с [поддержки Майкрософт][Support].</span><span class="sxs-lookup"><span data-stu-id="ef635-109">If Microsoft support is needed tooresolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef635-110">Данный документ является предполагаемым toohelp диагностики и исправления простой проблемы.</span><span class="sxs-lookup"><span data-stu-id="ef635-110">This document is intended toohelp diagnosing and fixing simple issues.</span></span> <span data-ttu-id="ef635-111">Это не toobe предназначен для замены технической поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ef635-111">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="ef635-112">Откройте запрос в службу поддержки с [поддержки Майкрософт] [ Support] Если проблему не удается toosolve hello, с помощью hello инструкциям.</span><span class="sxs-lookup"><span data-stu-id="ef635-112">Open a support ticket with [Microsoft Support][Support] if you are unable toosolve hello problem using hello guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="ef635-113">Обзор</span><span class="sxs-lookup"><span data-stu-id="ef635-113">Overview</span></span>
<span data-ttu-id="ef635-114">Hello следующей схеме показаны подключения логических hello сети tooMicrosoft сети клиента с помощью ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef635-114">hello following diagram shows hello logical connectivity of a customer network tooMicrosoft network using ExpressRoute.</span></span>
<span data-ttu-id="ef635-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="ef635-115">[![1]][1]</span></span>

<span data-ttu-id="ef635-116">В предшествующей схеме hello hello числа указывают точки ключа сети.</span><span class="sxs-lookup"><span data-stu-id="ef635-116">In hello preceding diagram, hello numbers indicate key network points.</span></span> <span data-ttu-id="ef635-117">Hello точке сети часто ссылки в этой статье на их соответствующее число.</span><span class="sxs-lookup"><span data-stu-id="ef635-117">hello network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="ef635-118">В зависимости от подключения ExpressRoute hello модели (совместного размещения в облаке Exchange, Ethernet-подключение между узлами или Any к any (IPVPN)) hello сети точки 3 и 4 могут быть коммутаторы (уровень 2 устройства).</span><span class="sxs-lookup"><span data-stu-id="ef635-118">Depending on hello ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) hello network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="ef635-119">точки ключа сетевой Hello показано выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ef635-119">hello key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="ef635-120">Клиентское вычислительное устройство (например, сервер или компьютер).</span><span class="sxs-lookup"><span data-stu-id="ef635-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="ef635-121">Клиентские пограничные маршрутизаторы (CE).</span><span class="sxs-lookup"><span data-stu-id="ef635-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="ef635-122">Пограничные маршрутизаторы (коммутаторы) поставщика услуг связи, подключенные к клиентским пограничным маршрутизаторам (PE, подключенные к CE).</span><span class="sxs-lookup"><span data-stu-id="ef635-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="ef635-123">Ссылка tooas PE CEs в этом документе.</span><span class="sxs-lookup"><span data-stu-id="ef635-123">Referred tooas PE-CEs in this document.</span></span>
4.  <span data-ttu-id="ef635-124">Пограничные маршрутизаторы (коммутаторы) поставщика услуг связи, подключенные к MSEE.</span><span class="sxs-lookup"><span data-stu-id="ef635-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="ef635-125">Ссылка tooas PE MSEEs в этом документе.</span><span class="sxs-lookup"><span data-stu-id="ef635-125">Referred tooas PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="ef635-126">Маршрутизаторы MSEE ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef635-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="ef635-127">Шлюз виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="ef635-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="ef635-128">Вычислений устройства на hello виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="ef635-128">Compute device on hello Azure VNet</span></span>

<span data-ttu-id="ef635-129">При использовании модели подключения к совместного размещения в облаке Exchange или Ethernet-подключение точка-точка hello пограничный маршрутизатор клиента hello (2) породит BGP пиринг с MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="ef635-129">If hello Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, hello customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="ef635-130">Точки сети 3 и 4 будут по-прежнему существовать, но будут в некоторой степени прозрачными как устройства уровня 2.</span><span class="sxs-lookup"><span data-stu-id="ef635-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="ef635-131">При использовании модели подключения к любой к any (IPVPN) hello hello синтаксические ошибки (с выходом MSEE) (4) породит BGP пиринг с MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="ef635-131">If hello Any-to-any (IPVPN) connectivity model is used, hello PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="ef635-132">Маршруты затем распространит задней toohello сети клиента через сети поставщика услуг IPVPN hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-132">Routes would then propagate back toohello customer network via hello IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="ef635-133">Для обеспечения высокой доступности ExpressRoute корпорации Майкрософт необходима избыточная пара сеансов BGP между маршрутизаторами MSEE (5) и маршрутизаторами поставщика услуг связи, подключенными к MSEE (PE-MSEE) (4).</span><span class="sxs-lookup"><span data-stu-id="ef635-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="ef635-134">Рекомендуется также избыточная пара сетевых путей между клиентской сетью и маршрутизаторами PE-CE.</span><span class="sxs-lookup"><span data-stu-id="ef635-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="ef635-135">Однако в модели подключения Any к any (IPVPN) одно устройство CE (2) возможно подключенных tooone или дополнительные синтаксические ошибки (3).</span><span class="sxs-lookup"><span data-stu-id="ef635-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected tooone or more PEs (3).</span></span>
>
>

<span data-ttu-id="ef635-136">(с точки сети hello обозначается hello связанный номер) рассматриваются toovalidate канал ExpressRoute hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ef635-136">toovalidate an ExpressRoute circuit, hello following steps are covered (with hello network point indicated by hello associated number):</span></span>
1. [<span data-ttu-id="ef635-137">Проверить подготовку и состояние канала (5).</span><span class="sxs-lookup"><span data-stu-id="ef635-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="ef635-138">Проверить, что настроен по крайней мере один пиринг ExpressRoute (5).</span><span class="sxs-lookup"><span data-stu-id="ef635-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="ef635-139">Проверка ARP между Майкрософт и hello поставщика услуг (связь между 4 и 5)</span><span class="sxs-lookup"><span data-stu-id="ef635-139">Validate ARP between Microsoft and hello service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="ef635-140">Проверка BGP и маршрутов на hello MSEE (BGP между 4 too5 и 5 too6, если подключение виртуальной сети)</span><span class="sxs-lookup"><span data-stu-id="ef635-140">Validate BGP and routes on hello MSEE (BGP between 4 too5, and 5 too6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="ef635-141">Проверьте hello статистике трафика (трафик, проходящий через 5)</span><span class="sxs-lookup"><span data-stu-id="ef635-141">Check hello Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="ef635-142">Дополнительные проверки и проверки будет добавлена в hello в будущем, посетите страницу ежемесячно!</span><span class="sxs-lookup"><span data-stu-id="ef635-142">More validations and checks will be added in hello future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="ef635-143">Проверка подготовки и состояния канала</span><span class="sxs-lookup"><span data-stu-id="ef635-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="ef635-144">Независимо от модели подключения к hello, канал ExpressRoute имеет toobe создан и, следовательно, службу создан для подготовки ключа.</span><span class="sxs-lookup"><span data-stu-id="ef635-144">Regardless of hello connectivity model, an ExpressRoute circuit has toobe created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="ef635-145">При подготовке канала ExpressRoute устанавливаются избыточные подключения уровня 2 между маршрутизаторами PE-MSEE (4) и MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="ef635-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="ef635-146">Дополнительные сведения о том, как toocreate, изменять, предоставить и проверить канал ExpressRoute. в статье hello [Создание и изменение канал ExpressRoute][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="ef635-146">For more information on how toocreate, modify, provision, and verify an ExpressRoute circuit, see hello article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="ef635-147">Ключ службы однозначно идентифицирует канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef635-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="ef635-148">Этот ключ является обязательным для большинства команд powershell hello, упомянутые в этом документе.</span><span class="sxs-lookup"><span data-stu-id="ef635-148">This key is required for most of hello powershell commands mentioned in this document.</span></span> <span data-ttu-id="ef635-149">Кроме того, следует вам нужна помощь от корпорации Майкрософт или из tootroubleshoot партнера ExpressRoute проблему ExpressRoute обслуживает hello ключа tooreadily идентификации hello канала.</span><span class="sxs-lookup"><span data-stu-id="ef635-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner tootroubleshoot an ExpressRoute issue, provide hello service key tooreadily identify hello circuit.</span></span>
>
>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="ef635-150">Проверка через портал Azure hello</span><span class="sxs-lookup"><span data-stu-id="ef635-150">Verification via hello Azure portal</span></span>
<span data-ttu-id="ef635-151">В hello портал Azure, можно проверить состояние hello канал ExpressRoute, выбрав ![2][2] на hello левой боковой панели меню, а затем выбрав hello канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef635-151">In hello Azure portal, hello status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="ef635-152">Выбор ExpressRoute цепи, перечисленных в разделе «Всех ресурсов» открывает колонку цепь ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-152">Selecting an ExpressRoute circuit listed under "All resources" opens hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="ef635-153">В hello ![3][3] раздел hello колонке hello essentials отображается, как показано на следующий снимок экрана приветствия ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="ef635-153">In hello ![3][3] section of hello blade, hello ExpressRoute essentials are listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="ef635-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="ef635-154">![4][4]</span></span>    

<span data-ttu-id="ef635-155">В ExpressRoute Essentials hello *Circuit состояние* указывает состояние hello hello канала на стороне Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-155">In hello ExpressRoute Essentials, *Circuit status* indicates hello status of hello circuit on hello Microsoft side.</span></span> <span data-ttu-id="ef635-156">*Поставщик состояния* указывает, был ли цепи hello *инициализировано или не подготовлены* на стороне поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-156">*Provider status* indicates if hello circuit has been *Provisioned/Not provisioned* on hello service-provider side.</span></span> 

<span data-ttu-id="ef635-157">ExpressRoute канала toobe оперативной, hello *Circuit состояние* должно быть *включено* и hello *состояние поставщика* должно быть *инициализировано*.</span><span class="sxs-lookup"><span data-stu-id="ef635-157">For an ExpressRoute circuit toobe operational, hello *Circuit status* must be *Enabled* and hello *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="ef635-158">Если hello *Circuit состояние* — не включено, обратитесь в службу [поддержки Майкрософт][Support].</span><span class="sxs-lookup"><span data-stu-id="ef635-158">If hello *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="ef635-159">Если hello *состояние поставщика* — не подготовлено, обратитесь к поставщику услуг.</span><span class="sxs-lookup"><span data-stu-id="ef635-159">If hello *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="ef635-160">Проверка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef635-160">Verification via PowerShell</span></span>
<span data-ttu-id="ef635-161">toolist все hello каналов ExpressRoute в группе ресурсов, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-161">toolist all hello ExpressRoute circuits in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="ef635-162">Имя группы ресурсов можно получить с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-162">You can get your resource group name through hello Azure portal.</span></span> <span data-ttu-id="ef635-163">Обратитесь к подразделу предыдущих hello в этом документе и обратите внимание, что имя группы ресурсов hello, указан снимок экрана примера hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-163">See hello previous subsection of this document and note that hello resource group name is listed in hello example screen shot.</span></span>
>
>

<span data-ttu-id="ef635-164">tooselect конкретного канала ExpressRoute в группе ресурсов hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ef635-164">tooselect a particular ExpressRoute circuit in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="ef635-165">Пример ответа:</span><span class="sxs-lookup"><span data-stu-id="ef635-165">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="ef635-166">tooconfirm, если канал ExpressRoute работоспособна, Обратите особое внимание toohello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="ef635-166">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="ef635-167">Если hello *параметр* — не включено, обратитесь в службу [поддержки Майкрософт][Support].</span><span class="sxs-lookup"><span data-stu-id="ef635-167">If hello *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="ef635-168">Если hello *ServiceProviderProvisioningState* — не подготовлено, обратитесь к поставщику услуг.</span><span class="sxs-lookup"><span data-stu-id="ef635-168">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="ef635-169">Проверка с помощью PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="ef635-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="ef635-170">toolist все hello каналов ExpressRoute в подписке, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-170">toolist all hello ExpressRoute circuits under a subscription, use hello following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="ef635-171">tooselect конкретного канала ExpressRoute, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ef635-171">tooselect a particular ExpressRoute circuit, use hello following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="ef635-172">Пример ответа:</span><span class="sxs-lookup"><span data-stu-id="ef635-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="ef635-173">tooconfirm, если канал ExpressRoute находится в рабочем состоянии, Обратите особое внимание toohello следующие поля: ServiceProviderProvisioningState: состояние подготовки: включено</span><span class="sxs-lookup"><span data-stu-id="ef635-173">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="ef635-174">Если hello *состояние* — не включено, обратитесь в службу [поддержки Майкрософт][Support].</span><span class="sxs-lookup"><span data-stu-id="ef635-174">If hello *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="ef635-175">Если hello *ServiceProviderProvisioningState* — не подготовлено, обратитесь к поставщику услуг.</span><span class="sxs-lookup"><span data-stu-id="ef635-175">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="ef635-176">Проверка настройки пиринга</span><span class="sxs-lookup"><span data-stu-id="ef635-176">Validate Peering Configuration</span></span>
<span data-ttu-id="ef635-177">После завершенного hello подготовки канал ExpressRoute hello hello поставщика услуг через hello канал ExpressRoute между MSEE-PR (4) и MSEEs (5) можно создать конфигурации маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="ef635-177">After hello service provider has completed hello provisioning hello ExpressRoute circuit, a routing configuration can be created over hello ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="ef635-178">Каждый канал ExpressRoute может иметь одно, два или три контексты маршрутизации включен: открытого пиринга Azure (трафик tooprivate виртуальных сетей в Azure), открытого пиринга Azure (IP-toopublic трафика адреса в Azure) и (трафик tooOffice 365 пиринг Майкрософт и Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="ef635-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic tooprivate virtual networks in Azure), Azure public peering (traffic toopublic IP addresses in Azure), and Microsoft peering (traffic tooOffice 365 and Dynamics 365).</span></span> <span data-ttu-id="ef635-179">Дополнительные сведения о том, как toocreate и изменить конфигурацию маршрутизации, см. в статье hello [Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ef635-179">For more information on how toocreate and modify routing configuration, see hello article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="ef635-180">Проверка через портал Azure hello</span><span class="sxs-lookup"><span data-stu-id="ef635-180">Verification via hello Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="ef635-181">В hello портал Azure, при котором пиринги ExpressRoute, имеется известная ошибка *не* отображаются на портале hello, если настроен поставщиком услуг hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-181">There is a known bug in hello Azure portal wherein ExpressRoute peerings are *NOT* shown in hello portal if configured by hello service provider.</span></span> <span data-ttu-id="ef635-182">Добавление пиринги ExpressRoute через портал hello или PowerShell *перезаписывает параметры поставщика службы hello*.</span><span class="sxs-lookup"><span data-stu-id="ef635-182">Adding ExpressRoute peerings via hello portal or PowerShell *overwrites hello service provider settings*.</span></span> <span data-ttu-id="ef635-183">Это действие прерывает hello маршрутизации на канал ExpressRoute hello и требуется поддержка hello параметров hello toorestore поставщика службы hello и восстановить нормальную маршрутизацию.</span><span class="sxs-lookup"><span data-stu-id="ef635-183">This action breaks hello routing on hello ExpressRoute circuit and requires hello support of hello service provider toorestore hello settings and reestablish normal routing.</span></span> <span data-ttu-id="ef635-184">Измените hello ExpressRoute пиринги только в том случае, если известно, что поставщик услуг, hello предоставляет только 2 уровня служб!</span><span class="sxs-lookup"><span data-stu-id="ef635-184">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="ef635-185">Если предоставлен уровня 3 с hello службы поставщика и hello пиринги пусты портале hello, PowerShell может быть используется toosee hello службы настроены параметры поставщика.</span><span class="sxs-lookup"><span data-stu-id="ef635-185">If layer 3 is provided by hello service provider and hello peerings are blank in hello portal, PowerShell can be used toosee hello service provider configured settings.</span></span>
>
>

<span data-ttu-id="ef635-186">В hello портал Azure, можно проверить состояние канала ExpressRoute, выбрав ![2][2] на hello левой боковой панели меню, а затем выбрав hello канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef635-186">In hello Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="ef635-187">Выбор ExpressRoute цепи, перечисленных в разделе «Всех ресурсов» будет открыт колонке цепь ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-187">Selecting an ExpressRoute circuit listed under "All resources" would open hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="ef635-188">В hello ![3][3] раздел hello колонке hello ExpressRoute, могут быть указаны essentials, как показано на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="ef635-188">In hello ![3][3] section of hello blade, hello ExpressRoute essentials would be listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="ef635-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="ef635-189">![5][5]</span></span>

<span data-ttu-id="ef635-190">В предыдущих пример hello как отмечено выше Azure закрытого пиринга маршрутизации контекста включен, в то время как открытые Azure и контексты маршрутизации пиринга Майкрософт не включен.</span><span class="sxs-lookup"><span data-stu-id="ef635-190">In hello preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="ef635-191">Успешно включен пиринга контекст также будет иметь подсетей основного и дополнительного точка-точка (требуется для протокола BGP) hello в списке.</span><span class="sxs-lookup"><span data-stu-id="ef635-191">A successfully enabled peering context would also have hello primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="ef635-192">Hello /30 подсети используются для IP-адрес интерфейса hello hello MSEEs и PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="ef635-192">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="ef635-193">Если пиринг не включена, убедитесь, если hello первичного и вторичного подсети назначены соответствуют конфигурации hello в PE-MSEEs.</span><span class="sxs-lookup"><span data-stu-id="ef635-193">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on PE-MSEEs.</span></span> <span data-ttu-id="ef635-194">Если нет, toochange hello конфигурации в MSEE маршрутизаторы, см. слишком[Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="ef635-194">If not, toochange hello configuration on MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="ef635-195">Проверка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef635-195">Verification via PowerShell</span></span>
<span data-ttu-id="ef635-196">tooget hello Azure закрытого пиринга сведения о конфигурации, используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ef635-196">tooget hello Azure private peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="ef635-197">Пример ответа в случае успешной настройки частного пиринга:</span><span class="sxs-lookup"><span data-stu-id="ef635-197">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="ef635-198">Успешно включен пиринга контекста будет иметь префиксов адреса основного и дополнительного hello в списке.</span><span class="sxs-lookup"><span data-stu-id="ef635-198">A successfully enabled peering context would have hello primary and secondary address prefixes listed.</span></span> <span data-ttu-id="ef635-199">Hello /30 подсети используются для IP-адрес интерфейса hello hello MSEEs и PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="ef635-199">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="ef635-200">tooget hello Azure открытый пиринг сведения о конфигурации, используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ef635-200">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="ef635-201">tooget hello Microsoft пиринга сведения о конфигурации, используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ef635-201">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="ef635-202">Если пиринг не настроен, отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="ef635-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="ef635-203">Образец ответа, когда hello указано пиринга (Azure открытый пиринг в этом примере) настроен в цепи hello:</span><span class="sxs-lookup"><span data-stu-id="ef635-203">A sample response, when hello stated peering (Azure Public peering in this example) is not configured within hello circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="ef635-204">Если пиринг не включена, проверьте при конфигурации hello подсетей основного и дополнительного назначенный соответствия hello на hello связаны PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="ef635-204">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="ef635-205">Также проверьте наличие hello исправить *VlanId*, *AzureASN*, и *PeerASN* применяются MSEEs и если эти значения сопоставляет toohello те на hello связаны PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="ef635-205">Also check if hello correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="ef635-206">Если вы выбрали хэширования MD5 hello общего ключа должны совпадать на пару MSEE и PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="ef635-206">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="ef635-207">конфигурации hello toochange на маршрутизаторах MSEE hello, см. слишком [создание и изменение маршрутизации для канала ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ef635-207">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="ef635-208">Проверка с помощью PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="ef635-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="ef635-209">tooget hello Azure закрытого пиринга сведения о конфигурации, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ef635-209">tooget hello Azure private peering configuration details, use hello following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="ef635-210">Пример ответа в случае успешной настройки частного пиринга:</span><span class="sxs-lookup"><span data-stu-id="ef635-210">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="ef635-211">Объект успешно, включен пиринга контекста будет иметь подсетей основного и дополнительного одноранговых hello в списке.</span><span class="sxs-lookup"><span data-stu-id="ef635-211">A successfully, enabled peering context would have hello primary and secondary peer subnets listed.</span></span> <span data-ttu-id="ef635-212">Hello /30 подсети используются для IP-адрес интерфейса hello hello MSEEs и PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="ef635-212">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="ef635-213">tooget hello Azure открытый пиринг сведения о конфигурации, используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ef635-213">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="ef635-214">tooget hello Microsoft пиринга сведения о конфигурации, используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ef635-214">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="ef635-215">Если пиринги уровня 3, заданные поставщиком услуг hello, установка hello пиринги ExpressRoute через портал hello или PowerShell перезаписывает hello параметры поставщика службы.</span><span class="sxs-lookup"><span data-stu-id="ef635-215">If layer 3 peerings were set by hello service provider, setting hello ExpressRoute peerings via hello portal or PowerShell overwrites hello service provider settings.</span></span> <span data-ttu-id="ef635-216">Сброс параметров пиринга стороне поставщика hello требуется поддержка hello hello поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="ef635-216">Resetting hello provider side peering settings requires hello support of hello service provider.</span></span> <span data-ttu-id="ef635-217">Измените hello ExpressRoute пиринги только в том случае, если известно, что поставщик услуг, hello предоставляет только 2 уровня служб!</span><span class="sxs-lookup"><span data-stu-id="ef635-217">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="ef635-218">Если пиринг не включена, проверьте при конфигурации hello первичного и вторичного одноранговых подсети назначены соответствия hello на hello связаны PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="ef635-218">If a peering is not enabled, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="ef635-219">Также проверьте наличие hello исправить *VlanId*, *AzureAsn*, и *PeerAsn* применяются MSEEs и если эти значения сопоставляет toohello те на hello связаны PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="ef635-219">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="ef635-220">конфигурации hello toochange на маршрутизаторах MSEE hello, см. слишком [создание и изменение маршрутизации для канала ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ef635-220">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a><span data-ttu-id="ef635-221">Проверка ARP между Майкрософт и hello поставщика услуг</span><span class="sxs-lookup"><span data-stu-id="ef635-221">Validate ARP between Microsoft and hello service provider</span></span>
<span data-ttu-id="ef635-222">В этом разделе используются классические команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef635-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="ef635-223">Если вы использовали команды PowerShell диспетчера ресурсов Azure, убедитесь, что доступ администратору или соадминистратору подписки toohello через [классический портал Azure][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="ef635-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="ef635-224">Устранение неполадок с помощью диспетчера ресурсов Azure команды можно найти toohello [начало ARP таблиц в модели развертывания диспетчера ресурсов hello] [ ARP] документа.</span><span class="sxs-lookup"><span data-stu-id="ef635-224">For troubleshooting using Azure Resource Manager commands please refer toohello [Getting ARP tables in hello Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="ef635-225">можно использовать tooget ARP hello портал Azure и команд PowerShell диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ef635-225">tooget ARP, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="ef635-226">При обнаружении ошибки с помощью команд PowerShell диспетчера ресурсов Azure hello, классический команд PowerShell должны работать в качестве классического PowerShell команды также работать с каналами ExpressRoute диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ef635-226">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="ef635-227">tooget hello таблицы ARP от основного маршрутизатора MSEE hello для частного пиринга hello, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-227">tooget hello ARP table from hello primary MSEE router for hello private peering, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="ef635-228">Пример ответа для команды hello, в случае успешного hello:</span><span class="sxs-lookup"><span data-stu-id="ef635-228">An example response for hello command, in hello successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="ef635-229">Аналогичным образом, можно проверить таблицы ARP из hello MSEE в hello hello *основной*/*получателя* пути, для *закрытый* /  *Открытый*/*Microsoft* пиринги.</span><span class="sxs-lookup"><span data-stu-id="ef635-229">Similarly, you can check hello ARP table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="ef635-230">Hello следующий пример, показано hello ответа hello команды для пиринга не существует.</span><span class="sxs-lookup"><span data-stu-id="ef635-230">hello following example shows hello response of hello command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="ef635-231">Если hello таблицы ARP отсутствует IP-адресов интерфейсов hello сопоставляются tooMAC адреса, hello просмотрите следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="ef635-231">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
>1. <span data-ttu-id="ef635-232">Если назначена hello первый IP-адрес подсети hello /30 для hello связь между hello MSEE PR и MSEE используется в интерфейсе hello MSEE PR.</span><span class="sxs-lookup"><span data-stu-id="ef635-232">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="ef635-233">Azure всегда использует hello второй IP-адрес для MSEEs.</span><span class="sxs-lookup"><span data-stu-id="ef635-233">Azure always uses hello second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="ef635-234">Убедитесь, если hello клиента (C-тег) и теги VLAN службы (S-Tag) соответствуют на пару MSEE PR и MSEE.</span><span class="sxs-lookup"><span data-stu-id="ef635-234">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a><span data-ttu-id="ef635-235">Проверка BGP и маршрутов на hello MSEE</span><span class="sxs-lookup"><span data-stu-id="ef635-235">Validate BGP and routes on hello MSEE</span></span>
<span data-ttu-id="ef635-236">В этом разделе используются классические команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef635-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="ef635-237">Если вы использовали команды PowerShell диспетчера ресурсов Azure, убедитесь, что доступ администратору или соадминистратору подписки toohello через [классический портал Azure][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="ef635-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="ef635-238">tooget BGP сведения, оба hello, можно использовать команды PowerShell диспетчера ресурсов Azure и портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ef635-238">tooget BGP information, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="ef635-239">При обнаружении ошибки с помощью команд PowerShell диспетчера ресурсов Azure hello, классический команд PowerShell должны работать в качестве классического PowerShell команды также работать с каналами ExpressRoute диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ef635-239">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="ef635-240">tooget hello таблицу маршрутизации (BGP сосед) сводки для определенного контекста маршрутизации, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-240">tooget hello routing table (BGP neighbor) summary for a particular routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="ef635-241">Пример ответа:</span><span class="sxs-lookup"><span data-stu-id="ef635-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="ef635-242">Как показано в предшествующих пример hello, команда hello является полезным toodetermine для длительность установки контекста маршрутизации hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-242">As shown in hello preceding example, hello command is useful toodetermine for how long hello routing context has been established.</span></span> <span data-ttu-id="ef635-243">Также указывается число префиксов маршрутов объявлены пиринга маршрутизатором hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-243">It also indicates number of route prefixes advertised by hello peering router.</span></span>

>[!NOTE]
><span data-ttu-id="ef635-244">Если состояние hello в активной работы или простоя, проверьте при конфигурации hello первичного и вторичного одноранговых подсети назначены соответствия hello на hello связаны PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="ef635-244">If hello state is in Active or Idle, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="ef635-245">Также проверьте наличие hello исправить *VlanId*, *AzureAsn*, и *PeerAsn* применяются MSEEs и если эти значения сопоставляет toohello те на hello связаны PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="ef635-245">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="ef635-246">Если вы выбрали хэширования MD5 hello общего ключа должны совпадать на пару MSEE и PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="ef635-246">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="ef635-247">конфигурации hello toochange на маршрутизаторах MSEE hello, см. слишком[Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ef635-247">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="ef635-248">Если определенные назначения недоступны через определенный пиринг, проверьте hello таблицы маршрутов из MSEEs hello, принадлежащие данному контексту пиринга toohello.</span><span class="sxs-lookup"><span data-stu-id="ef635-248">If certain destinations are not reachable over a particular peering, check hello route table of hello MSEEs belonging toohello particular peering context.</span></span> <span data-ttu-id="ef635-249">Если соответствующий префикс (возможно, NATed IP) присутствует в таблице маршрутизации hello, затем проверьте существуют брандмауэры, ACL или NSG по пути hello и разрешать или запрещать трафик hello.</span><span class="sxs-lookup"><span data-stu-id="ef635-249">If a matching prefix (could be NATed IP) is present in hello routing table, then check if there are firewalls/NSG/ACLs on hello path and if they permit hello traffic.</span></span>
>
>

<span data-ttu-id="ef635-250">tooget hello полной таблицы маршрутизации из MSEE hello *основной* путь для конкретного hello *закрытый* маршрутизации контекста, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ef635-250">tooget hello full routing table from MSEE on hello *Primary* path for hello particular *Private* routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="ef635-251">Пример успешный результат для hello команды является:</span><span class="sxs-lookup"><span data-stu-id="ef635-251">An example successful outcome for hello command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="ef635-252">Аналогичным образом, можно проверить таблицы маршрутизации hello из hello MSEE в hello *основной*/*получателя* пути, для *закрытый* / *Открытый*/*Microsoft* пиринга контекста.</span><span class="sxs-lookup"><span data-stu-id="ef635-252">Similarly, you can check hello routing table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="ef635-253">Hello следующий пример, показано hello ответа hello команды для пиринга не существует:</span><span class="sxs-lookup"><span data-stu-id="ef635-253">hello following example shows hello response of hello command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a><span data-ttu-id="ef635-254">Проверьте hello статистики</span><span class="sxs-lookup"><span data-stu-id="ef635-254">Check hello Traffic Statistics</span></span>
<span data-ttu-id="ef635-255">tooget hello вместе статистике трафика основной и дополнительный путь--байт и выхода из системы--пиринга контекста hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ef635-255">tooget hello combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="ef635-256">Пример выходных данных команды hello является:</span><span class="sxs-lookup"><span data-stu-id="ef635-256">A sample output of hello command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="ef635-257">Пример выходных данных команды hello для пиринга несуществующий является:</span><span class="sxs-lookup"><span data-stu-id="ef635-257">A sample output of hello command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="ef635-258">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ef635-258">Next Steps</span></span>
<span data-ttu-id="ef635-259">Для получения дополнительных сведений справки ознакомьтесь с hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="ef635-259">For more information or help, check out hello following links:</span></span>

- <span data-ttu-id="ef635-260">[Служба технической поддержки Майкрософт][Support]</span><span class="sxs-lookup"><span data-stu-id="ef635-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="ef635-261">[Создание и изменение канала ExpressRoute][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="ef635-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="ef635-262">[Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="ef635-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Логическое подключение ExpressRoute"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Значок "Все ресурсы""
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Значок "Обзор""
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Снимок экран раздела с основными сведениями об ExpressRoute"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Снимок экран раздела с основными сведениями об ExpressRoute"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






