---
title: "aaaWorkflows для настройки канала ExpressRoute | Документы Microsoft"
description: "Эта страница поможет выполнить hello рабочих процессов для настройки канал ExpressRoute и пиринги"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="20af7-103">Процедуры ExpressRoute для подготовки каналов и состояний каналов</span><span class="sxs-lookup"><span data-stu-id="20af7-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="20af7-104">Эта страница поможет выполнить подготовку службы hello и рабочие процессы маршрутизации конфигурации на высоком уровне.</span><span class="sxs-lookup"><span data-stu-id="20af7-104">This page walks you through hello service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="20af7-105">Hello ниже рисунок и соответствующие шаги Показать hello задачи должны следовать в порядке toohave ExpressRoute цепь подготовленных узел узел.</span><span class="sxs-lookup"><span data-stu-id="20af7-105">hello following figure and corresponding steps show hello tasks you must follow in order toohave an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="20af7-106">С помощью PowerShell tooconfigure канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20af7-106">Use PowerShell tooconfigure an ExpressRoute circuit.</span></span> <span data-ttu-id="20af7-107">Следуйте инструкциям hello hello [каналы ExpressRoute создания](expressroute-howto-circuit-classic.md) Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="20af7-107">Follow hello instructions in hello [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="20af7-108">Порядок подключения поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="20af7-108">Order connectivity from hello service provider.</span></span> <span data-ttu-id="20af7-109">Порядок действий может варьироваться.</span><span class="sxs-lookup"><span data-stu-id="20af7-109">This process varies.</span></span> <span data-ttu-id="20af7-110">Обратитесь к поставщику услуг подключения, Дополнительные сведения о том, как tooorder подключения.</span><span class="sxs-lookup"><span data-stu-id="20af7-110">Contact your connectivity provider for more details about how tooorder connectivity.</span></span>
3. <span data-ttu-id="20af7-111">Убедитесь, что hello цепь была подготовлена успешно, проверяя состояние через PowerShell подготовки канал ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="20af7-111">Ensure that hello circuit has been provisioned successfully by verifying hello ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="20af7-112">Настройте домены маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="20af7-112">Configure routing domains.</span></span> <span data-ttu-id="20af7-113">Если ваш поставщик услуг подключения выполняет для вас управление третьего уровня, он настроит и маршрутизацию для вашего канала.</span><span class="sxs-lookup"><span data-stu-id="20af7-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="20af7-114">Если поставщиком соединения только предлагает второго уровня службы, необходимо настроить маршрутизации по инструкциям, описанным в hello [требования к маршрутизации](expressroute-routing.md) и [конфигурации маршрутизации](expressroute-howto-routing-classic.md) страниц.</span><span class="sxs-lookup"><span data-stu-id="20af7-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in hello [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="20af7-115">Включить открытого пиринга Azure — необходимо включить этот пиринг tooVMs tooconnect / облачных служб, развернутых в виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="20af7-115">Enable Azure private peering - You must enable this peering tooconnect tooVMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="20af7-116">Включить частного пиринга Azure — необходимо включить частного пиринга Azure при желании tooconnect tooAzure службами, размещенными на общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="20af7-116">Enable Azure public peering - You must enable Azure public peering if you wish tooconnect tooAzure services hosted on public IP addresses.</span></span> <span data-ttu-id="20af7-117">Это требование tooaccess ресурсы Azure, если вы выбрали tooenable Маршрутизация по умолчанию для открытого пиринга Azure.</span><span class="sxs-lookup"><span data-stu-id="20af7-117">This is a requirement tooaccess Azure resources if you have chosen tooenable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="20af7-118">Включить пиринг Майкрософт — это tooaccess Office 365 и Dynamics 365, необходимо включить.</span><span class="sxs-lookup"><span data-stu-id="20af7-118">Enable Microsoft peering - You must enable this tooaccess Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="20af7-119">Необходимо убедиться, используется отдельный прокси / edge tooconnect tooMicrosoft, чем то, которое используется для hello hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="20af7-119">You must ensure that you use a separate proxy / edge tooconnect tooMicrosoft than hello one you use for hello Internet.</span></span> <span data-ttu-id="20af7-120">С помощью hello же краю для ExpressRoute и hello Интернет приведут асимметричного маршрутизации и причиной простоев подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="20af7-120">Using hello same edge for both ExpressRoute and hello Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="20af7-121">Связывание виртуальной сети цепи tooExpressRoute - можно связать канал ExpressRoute tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="20af7-121">Linking virtual networks tooExpressRoute circuits - You can link virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="20af7-122">Следуйте инструкциям [toolink виртуальных сетей](expressroute-howto-linkvnet-arm.md) tooyour канала.</span><span class="sxs-lookup"><span data-stu-id="20af7-122">Follow instructions [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span></span> <span data-ttu-id="20af7-123">Эти виртуальные сети могут быть либо в ту же подписку Azure канал ExpressRoute hello hello, или может быть в другую подписку.</span><span class="sxs-lookup"><span data-stu-id="20af7-123">These VNets can either be in hello same Azure subscription as hello ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="20af7-124">Состояния подготовки канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="20af7-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="20af7-125">У каждого канала ExpressRoute имеется два состояния.</span><span class="sxs-lookup"><span data-stu-id="20af7-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="20af7-126">Состояние подготовки поставщика услуг</span><span class="sxs-lookup"><span data-stu-id="20af7-126">Service provider provisioning state</span></span>
* <span data-ttu-id="20af7-127">Состояние</span><span class="sxs-lookup"><span data-stu-id="20af7-127">Status</span></span>

<span data-ttu-id="20af7-128">Состояние указывает на состояние подготовки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="20af7-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="20af7-129">Это свойство имеет значение tooEnabled при создании канала Expressroute</span><span class="sxs-lookup"><span data-stu-id="20af7-129">This property is set tooEnabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="20af7-130">состояние подготовки поставщика подключения Hello представляет состояние hello на стороне поставщика услуг подключения hello.</span><span class="sxs-lookup"><span data-stu-id="20af7-130">hello connectivity provider provisioning state represents hello state on hello connectivity provider's side.</span></span> <span data-ttu-id="20af7-131">Возможные состояния: *NotProvisioned* (Не подготовлен), *Provisioning* (Идет подготовка) и *Provisioned* (Подготовлен).</span><span class="sxs-lookup"><span data-stu-id="20af7-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="20af7-132">Hello канал ExpressRoute должна находиться в состоянии подготовлена для вас toobe может toouse его.</span><span class="sxs-lookup"><span data-stu-id="20af7-132">hello ExpressRoute circuit must be in Provisioned state for you toobe able toouse it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="20af7-133">Возможные состояния канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="20af7-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="20af7-134">В этом разделе перечислены возможные состояния hello за канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20af7-134">This section lists out hello possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="20af7-135">**В момент создания**</span><span class="sxs-lookup"><span data-stu-id="20af7-135">**At creation time**</span></span>

<span data-ttu-id="20af7-136">Вы увидите hello каналов expressroute в hello следующие состояния, как только вы запустите hello hello PowerShell командлет toocreate канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20af7-136">You will see hello ExpressRoute circuit in hello following state as soon as you run hello PowerShell cmdlet toocreate hello ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="20af7-137">**Если поставщика услуг подключения находится в процесс подготовки канала hello hello**</span><span class="sxs-lookup"><span data-stu-id="20af7-137">**When connectivity provider is in hello process of provisioning hello circuit**</span></span>

<span data-ttu-id="20af7-138">Вы увидите hello каналов expressroute в hello, как только вы следующие состояния передачи поставщика услуг подключения ключа toohello службы hello и запуска процесса инициализации hello.</span><span class="sxs-lookup"><span data-stu-id="20af7-138">You will see hello ExpressRoute circuit in hello following state as soon as you pass hello service key toohello connectivity provider and they have started hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="20af7-139">**После завершения процесса подготовки hello поставщика услуг подключения**</span><span class="sxs-lookup"><span data-stu-id="20af7-139">**When connectivity provider has completed hello provisioning process**</span></span>

<span data-ttu-id="20af7-140">Вы увидите hello канал ExpressRoute в следующие состояния сразу же после завершения hello процесса инициализации поставщика услуг подключения hello hello.</span><span class="sxs-lookup"><span data-stu-id="20af7-140">You will see hello ExpressRoute circuit in hello following state as soon as hello connectivity provider has completed hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="20af7-141">Подготовить и включить — hello цепи hello состояние может быть только в для вас toobe может toouse его.</span><span class="sxs-lookup"><span data-stu-id="20af7-141">Provisioned and Enabled is hello only state hello circuit can be in for you toobe able toouse it.</span></span> <span data-ttu-id="20af7-142">Если ваш поставщик предлагает услуги второго уровня, вы можете настроить маршрутизацию для канала, только если он находится в этом состоянии.</span><span class="sxs-lookup"><span data-stu-id="20af7-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="20af7-143">**Если поставщика услуг подключения отзывает hello канала**</span><span class="sxs-lookup"><span data-stu-id="20af7-143">**When connectivity provider is deprovisioning hello circuit**</span></span>

<span data-ttu-id="20af7-144">Если вы запросили hello службы поставщика toodeprovision hello каналом expressroute, вы увидите цепи hello набора toohello следующие состояния после завершения hello отзыва процесса hello поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="20af7-144">If you requested hello service provider toodeprovision hello ExpressRoute circuit, you will see hello circuit set toohello following state after hello service provider has completed hello deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="20af7-145">Вы можете включить toore его при необходимости или запускать командлеты PowerShell toodelete hello канала.</span><span class="sxs-lookup"><span data-stu-id="20af7-145">You can choose toore-enable it if needed, or run PowerShell cmdlets toodelete hello circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="20af7-146">При запуске hello toodelete hello командлет PowerShell канала, при операции hello подготовки или инициализировано hello ServiceProviderProvisioningState завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="20af7-146">If you run hello PowerShell cmdlet toodelete hello circuit when hello ServiceProviderProvisioningState is Provisioning or Provisioned hello operation will fail.</span></span> <span data-ttu-id="20af7-147">Обратитесь к каналу ExpressRoute поставщика toodeprovision подключения hello сначала и затем удалить цепь hello.</span><span class="sxs-lookup"><span data-stu-id="20af7-147">Please work with your connectivity provider toodeprovision hello ExpressRoute circuit first and then delete hello circuit.</span></span> <span data-ttu-id="20af7-148">Корпорация Майкрософт будет toobill hello канала до запуска hello цепи hello toodelete командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20af7-148">Microsoft will continue toobill hello circuit until you run hello PowerShell cmdlet toodelete hello circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="20af7-149">Состояние конфигурации сеанса маршрутизации</span><span class="sxs-lookup"><span data-stu-id="20af7-149">Routing session configuration state</span></span>
<span data-ttu-id="20af7-150">состояние подготовки BGP Hello позволяет узнать, если сеанс BGP hello была включена hello Microsoft edge.</span><span class="sxs-lookup"><span data-stu-id="20af7-150">hello BGP provisioning state lets you know if hello BGP session has been enabled on hello Microsoft edge.</span></span> <span data-ttu-id="20af7-151">Hello состояния должна быть включена для вас toobe может toouse hello пиринга.</span><span class="sxs-lookup"><span data-stu-id="20af7-151">hello state must be enabled for you toobe able toouse hello peering.</span></span>

<span data-ttu-id="20af7-152">Это состояние сеанса BGP hello важные toocheck специально для пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="20af7-152">It is important toocheck hello BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="20af7-153">В дополнение toohello BGP состояние подготовки, имеется другое состояние — *объявленных открытых префиксов состояние*.</span><span class="sxs-lookup"><span data-stu-id="20af7-153">In addition toohello BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="20af7-154">Hello объявленных открытых префиксов состояние должно быть в *настроен* состояния, как для toobe сеанса BGP hello вверх и вашей маршрутизации toowork end-to-end.</span><span class="sxs-lookup"><span data-stu-id="20af7-154">hello advertised public prefixes state must be in *configured* state, both for hello BGP session toobe up and for your routing toowork end-to-end.</span></span> 

<span data-ttu-id="20af7-155">Если hello объявленных состояние открытого префикс имеет tooa *проверки необходимости* состояние сеанса BGP hello не включена, как hello объявленные префиксы не совпали hello как число, в каком-либо маршрутизации реестров hello.</span><span class="sxs-lookup"><span data-stu-id="20af7-155">If hello advertised public prefix state is set tooa *validation needed* state, hello BGP session is not enabled, as hello advertised prefixes did not match hello AS number in any of hello routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="20af7-156">Если hello объявленных открытых префиксов состояния находится в *Ручная проверка* состояние, необходимо открыть запрос в службу поддержки с [поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) и предоставить свидетельство своих IP-адресов hello объявленных вдоль с hello связанный номер автономной системы.</span><span class="sxs-lookup"><span data-stu-id="20af7-156">If hello advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own hello IP addresses advertised along with hello associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="20af7-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="20af7-157">Next steps</span></span>
* <span data-ttu-id="20af7-158">Настройте подключение ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20af7-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="20af7-159">Создайте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20af7-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="20af7-160">Настройка маршрутизации</span><span class="sxs-lookup"><span data-stu-id="20af7-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="20af7-161">Связывание виртуальной сети tooan канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="20af7-161">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

