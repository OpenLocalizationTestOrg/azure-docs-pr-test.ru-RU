---
title: "Процедуры настройки канала ExpressRoute | Документация Майкрософт"
description: "На этой странице описана процедура настройки канала ExpressRoute и пирингов"
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
ms.openlocfilehash: cba1b2cfee379e7d2b079bcb3089981ef1044d66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="6e6d8-103">Процедуры ExpressRoute для подготовки каналов и состояний каналов</span><span class="sxs-lookup"><span data-stu-id="6e6d8-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="6e6d8-104">На этой странице описаны процедуры подготовки служб и настройки маршрутизации на высоком уровне.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-104">This page walks you through the service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="6e6d8-105">Приведенная схема и соответствующие действия показывают, какие задачи нужно выполнить, чтобы полностью подготовить канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-105">The following figure and corresponding steps show the tasks you must follow in order to have an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="6e6d8-106">Настройте канал ExpressRoute с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-106">Use PowerShell to configure an ExpressRoute circuit.</span></span> <span data-ttu-id="6e6d8-107">Для этого выполните инструкции в статье [Создание каналов ExpressRoute](expressroute-howto-circuit-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="6e6d8-107">Follow the instructions in the [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="6e6d8-108">Закажите подключение у поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-108">Order connectivity from the service provider.</span></span> <span data-ttu-id="6e6d8-109">Порядок действий может варьироваться.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-109">This process varies.</span></span> <span data-ttu-id="6e6d8-110">За подробной информацией о заказе подключения обратитесь к поставщику услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-110">Contact your connectivity provider for more details about how to order connectivity.</span></span>
3. <span data-ttu-id="6e6d8-111">Убедитесь, что канал был подготовлен, проверив состояние подготовки канала ExpressRoute с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-111">Ensure that the circuit has been provisioned successfully by verifying the ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="6e6d8-112">Настройте домены маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-112">Configure routing domains.</span></span> <span data-ttu-id="6e6d8-113">Если ваш поставщик услуг подключения выполняет для вас управление третьего уровня, он настроит и маршрутизацию для вашего канала.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="6e6d8-114">Если поставщик услуг подключения предлагает только услуги второго уровня, настройте маршрутизацию согласно инструкциям на страницах [Требования к маршрутизации](expressroute-routing.md) и [Настройка маршрутизации](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="6e6d8-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in the [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="6e6d8-115">Включите частный пиринг Azure — он требуется для подключения к виртуальным машинам и (или) облачным службам, развернутым в виртуальных сетях.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-115">Enable Azure private peering - You must enable this peering to connect to VMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="6e6d8-116">Включите общедоступный пиринг Azure — он нужен в случае, если вы захотите подключиться к службам Azure, размещенным по общедоступным IP-адресам.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-116">Enable Azure public peering - You must enable Azure public peering if you wish to connect to Azure services hosted on public IP addresses.</span></span> <span data-ttu-id="6e6d8-117">Включение этого пиринга требуется для доступа к ресурсам Azure, если для частного пиринга Azure вы выбрали маршрутизацию по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-117">This is a requirement to access Azure resources if you have chosen to enable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="6e6d8-118">Включите пиринг Майкрософт — он требуется для доступа к Office 365 и Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-118">Enable Microsoft peering - You must enable this to access Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="6e6d8-119">Для подключения к Майкрософт нельзя использовать прокси-сервер или ресурс, который используется для подключения к Интернету.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-119">You must ensure that you use a separate proxy / edge to connect to Microsoft than the one you use for the Internet.</span></span> <span data-ttu-id="6e6d8-120">Подключение к ExpressRoute и к Интернету через один и тот же ресурс приведет к асимметричной маршрутизации и вызовет проблемы подключения в вашей сети.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-120">Using the same edge for both ExpressRoute and the Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="6e6d8-121">Свяжите виртуальные сети с каналами ExpressRoute. Виртуальные сети можно связать с каналом ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-121">Linking virtual networks to ExpressRoute circuits - You can link virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="6e6d8-122">Выполните инструкции по [связыванию виртуальных сетей](expressroute-howto-linkvnet-arm.md) с каналом.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-122">Follow instructions [to link VNets](expressroute-howto-linkvnet-arm.md) to your circuit.</span></span> <span data-ttu-id="6e6d8-123">Эти виртуальные сети могут входить в ту же самую подписку, что и канал ExpressRoute, или в другую.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-123">These VNets can either be in the same Azure subscription as the ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="6e6d8-124">Состояния подготовки канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6e6d8-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="6e6d8-125">У каждого канала ExpressRoute имеется два состояния.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="6e6d8-126">Состояние подготовки поставщика услуг</span><span class="sxs-lookup"><span data-stu-id="6e6d8-126">Service provider provisioning state</span></span>
* <span data-ttu-id="6e6d8-127">Состояние</span><span class="sxs-lookup"><span data-stu-id="6e6d8-127">Status</span></span>

<span data-ttu-id="6e6d8-128">Состояние указывает на состояние подготовки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="6e6d8-129">При создании канала Expressroute это свойство имеет значение "Включен".</span><span class="sxs-lookup"><span data-stu-id="6e6d8-129">This property is set to Enabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="6e6d8-130">Состояние подготовки поставщика услуг подключения обозначает состояние на стороне поставщика.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-130">The connectivity provider provisioning state represents the state on the connectivity provider's side.</span></span> <span data-ttu-id="6e6d8-131">Возможные состояния: *NotProvisioned* (Не подготовлен), *Provisioning* (Идет подготовка) и *Provisioned* (Подготовлен).</span><span class="sxs-lookup"><span data-stu-id="6e6d8-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="6e6d8-132">Для того чтобы канал ExpressRoute можно было использовать, он должен находиться в состоянии Provisioned (Подготовлен).</span><span class="sxs-lookup"><span data-stu-id="6e6d8-132">The ExpressRoute circuit must be in Provisioned state for you to be able to use it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="6e6d8-133">Возможные состояния канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6e6d8-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="6e6d8-134">В этом разделе перечислены возможные состояния канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-134">This section lists out the possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="6e6d8-135">**В момент создания**</span><span class="sxs-lookup"><span data-stu-id="6e6d8-135">**At creation time**</span></span>

<span data-ttu-id="6e6d8-136">После выполнения командлета PowerShell для создания канала ExpressRoute канал ExpressRoute будет находиться в следующем состоянии:</span><span class="sxs-lookup"><span data-stu-id="6e6d8-136">You will see the ExpressRoute circuit in the following state as soon as you run the PowerShell cmdlet to create the ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="6e6d8-137">**Пока поставщик услуг подключения выполняет подготовку канала**</span><span class="sxs-lookup"><span data-stu-id="6e6d8-137">**When connectivity provider is in the process of provisioning the circuit**</span></span>

<span data-ttu-id="6e6d8-138">Когда вы передадите ключ службы поставщику услуг подключения, а тот начнет процесс подготовки, канал ExpressRoute перейдет в следующее состояние:</span><span class="sxs-lookup"><span data-stu-id="6e6d8-138">You will see the ExpressRoute circuit in the following state as soon as you pass the service key to the connectivity provider and they have started the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="6e6d8-139">**После завершения процесса подготовки поставщиком услуг подключения**</span><span class="sxs-lookup"><span data-stu-id="6e6d8-139">**When connectivity provider has completed the provisioning process**</span></span>

<span data-ttu-id="6e6d8-140">Когда поставщик услуг подключения закончит процесс подготовки, канал ExpressRoute перейдет в следующее состояние:</span><span class="sxs-lookup"><span data-stu-id="6e6d8-140">You will see the ExpressRoute circuit in the following state as soon as the connectivity provider has completed the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="6e6d8-141">Использовать канал позволяют только два его состояния: Provisioned (Подготовлен) и Enabled (Включен).</span><span class="sxs-lookup"><span data-stu-id="6e6d8-141">Provisioned and Enabled is the only state the circuit can be in for you to be able to use it.</span></span> <span data-ttu-id="6e6d8-142">Если ваш поставщик предлагает услуги второго уровня, вы можете настроить маршрутизацию для канала, только если он находится в этом состоянии.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="6e6d8-143">**Пока поставщик услуг подключения отзывает канал**</span><span class="sxs-lookup"><span data-stu-id="6e6d8-143">**When connectivity provider is deprovisioning the circuit**</span></span>

<span data-ttu-id="6e6d8-144">Если вы обратились по поводу отзыва канала ExpressRoute к поставщику услуг, то после того, как он завершит процедуру отзыва, канал перейдет в следующее состояние:</span><span class="sxs-lookup"><span data-stu-id="6e6d8-144">If you requested the service provider to deprovision the ExpressRoute circuit, you will see the circuit set to the following state after the service provider has completed the deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="6e6d8-145">При необходимости вы можете снова включить канал или удалить его с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-145">You can choose to re-enable it if needed, or run PowerShell cmdlets to delete the circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="6e6d8-146">Если запустить командлет PowerShell для удаления канала в тот момент, когда параметр ServiceProviderProvisioningState находится в состоянии "Идет подготовка" или "Подготовлен", то операция завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-146">If you run the PowerShell cmdlet to delete the circuit when the ServiceProviderProvisioningState is Provisioning or Provisioned the operation will fail.</span></span> <span data-ttu-id="6e6d8-147">Обратитесь к своему поставщику услуг подключения, чтобы сначала отозвать, а затем удалить канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-147">Please work with your connectivity provider to deprovision the ExpressRoute circuit first and then delete the circuit.</span></span> <span data-ttu-id="6e6d8-148">Корпорация Майкрософт будет выставлять вам счета за канал, пока вы не выполните командлет PowerShell для его удаления.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-148">Microsoft will continue to bill the circuit until you run the PowerShell cmdlet to delete the circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="6e6d8-149">Состояние конфигурации сеанса маршрутизации</span><span class="sxs-lookup"><span data-stu-id="6e6d8-149">Routing session configuration state</span></span>
<span data-ttu-id="6e6d8-150">Состояние подготовки BGP позволяет вам узнать, что сеанс BGP был включен на стороне Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-150">The BGP provisioning state lets you know if the BGP session has been enabled on the Microsoft edge.</span></span> <span data-ttu-id="6e6d8-151">Пиринг можно использовать, только если состояние включено.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-151">The state must be enabled for you to be able to use the peering.</span></span>

<span data-ttu-id="6e6d8-152">Обязательно проверьте состояние сеанса BGP, особенно для пиринга Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-152">It is important to check the BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="6e6d8-153">Еще одно состояние, которое нужно учитывать, называется *состояние объявленных общедоступных префиксов*.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-153">In addition to the BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="6e6d8-154">Для работы сеанса BGP и полноценной работы маршрутизации состояние объявленных общедоступных префиксов должно иметь значение *Configured* .</span><span class="sxs-lookup"><span data-stu-id="6e6d8-154">The advertised public prefixes state must be in *configured* state, both for the BGP session to be up and for your routing to work end-to-end.</span></span> 

<span data-ttu-id="6e6d8-155">Если для состояния объявленных общедоступных префиксов установлено значение *Validation needed* (Требуется проверка), сеанс BGP не включается, поскольку объявленные префиксы не совпадают с номером AS ни в одном реестре маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-155">If the advertised public prefix state is set to a *validation needed* state, the BGP session is not enabled, as the advertised prefixes did not match the AS number in any of the routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6e6d8-156">Если для состояния объявленных общедоступных префиксов имеет значение *Manual validation* (Ручная проверка), необходимо создать запрос в [службу поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) и предоставить документы, подтверждающие ваше владение объявленными IP-адресами и связанным с ними номером автономной системы.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-156">If the advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own the IP addresses advertised along with the associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6e6d8-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e6d8-157">Next steps</span></span>
* <span data-ttu-id="6e6d8-158">Настройте подключение ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="6e6d8-159">Создайте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6e6d8-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="6e6d8-160">Настройка маршрутизации</span><span class="sxs-lookup"><span data-stu-id="6e6d8-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="6e6d8-161">Связывание виртуальной сети с каналом ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6e6d8-161">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

