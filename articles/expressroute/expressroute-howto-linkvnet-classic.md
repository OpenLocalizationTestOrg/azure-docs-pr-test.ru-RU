---
title: "Связывание виртуальной сети tooan канал ExpressRoute: PowerShell: классический: Azure | Документы Microsoft"
description: "Этот документ содержит общие сведения о том, как toolink виртуальных сетей (Vnet) tooExpressRoute цепи с помощью hello классической модели развертывания и PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="fba1d-103">Подключиться с помощью PowerShell (классические) канал ExpressRoute tooan виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="fba1d-103">Connect a virtual network tooan ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fba1d-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="fba1d-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="fba1d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fba1d-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="fba1d-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="fba1d-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="fba1d-107">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="fba1d-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="fba1d-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="fba1d-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="fba1d-109">Эта статья поможет вам связать каналы ExpressRoute tooAzure виртуальных сетей (Vnet) с помощью hello классической модели развертывания и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fba1d-109">This article will help you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello classic deployment model and PowerShell.</span></span> <span data-ttu-id="fba1d-110">Виртуальные сети может быть либо в одной подписке hello или может быть частью другой подписки.</span><span class="sxs-lookup"><span data-stu-id="fba1d-110">Virtual networks can either be in hello same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="fba1d-111">**О моделях развертывания Azure**</span><span class="sxs-lookup"><span data-stu-id="fba1d-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="fba1d-112">Предварительные требования для настройки</span><span class="sxs-lookup"><span data-stu-id="fba1d-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="fba1d-113">Требуется последняя версия hello hello модули Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fba1d-113">You need hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="fba1d-114">Hello последнюю модули PowerShell можно загрузить из hello PowerShell раздел hello [страницу загрузок Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fba1d-114">You can download hello latest PowerShell modules from hello PowerShell section of hello [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="fba1d-115">Следуйте инструкциям в разделе hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) пошаговые инструкции о том, как tooconfigure модули Azure PowerShell hello toouse компьютера.</span><span class="sxs-lookup"><span data-stu-id="fba1d-115">Follow hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>
2. <span data-ttu-id="fba1d-116">Требуется tooreview hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="fba1d-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="fba1d-117">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fba1d-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="fba1d-118">Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-classic.md) и иметь поставщиком соединения включить hello канала.</span><span class="sxs-lookup"><span data-stu-id="fba1d-118">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable hello circuit.</span></span>
   * <span data-ttu-id="fba1d-119">Убедитесь, что для вашего канала настроен частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="fba1d-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="fba1d-120">В разделе hello [Настройка маршрутизации](expressroute-howto-routing-classic.md) маршрутизации инструкции.</span><span class="sxs-lookup"><span data-stu-id="fba1d-120">See hello [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="fba1d-121">Убедитесь, что настроен открытого пиринга Azure и hello пиринга BGP между вашей сетью и Майкрософт работает так, чтобы можно было включить подключение начала до конца.</span><span class="sxs-lookup"><span data-stu-id="fba1d-121">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="fba1d-122">Вам необходимо иметь созданные и полностью подготовленные виртуальную сеть и шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fba1d-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="fba1d-123">Следуйте инструкциям hello слишком[Настройка виртуальной сети для ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="fba1d-123">Follow hello instructions too[configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="fba1d-124">Объедините tooan виртуальных сетей too10 канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fba1d-124">You can link up too10 virtual networks tooan ExpressRoute circuit.</span></span> <span data-ttu-id="fba1d-125">Все виртуальные сети должны быть в hello геополитические совпадают.</span><span class="sxs-lookup"><span data-stu-id="fba1d-125">All virtual networks must be in hello same geopolitical region.</span></span> <span data-ttu-id="fba1d-126">Можно связать большее количество виртуальных сетей tooyour канал ExpressRoute или связать виртуальных сетей, которые находятся в других геополитических регионов, если вы включили hello ExpressRoute премиальное дополнение.</span><span class="sxs-lookup"><span data-stu-id="fba1d-126">You can link a larger number of virtual networks tooyour ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="fba1d-127">Проверьте hello [часто задаваемые вопросы о](expressroute-faqs.md) Дополнительные сведения о премиальное дополнение hello.</span><span class="sxs-lookup"><span data-stu-id="fba1d-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="fba1d-128">Подключить виртуальную сеть в Привет одному каналу tooa подписки</span><span class="sxs-lookup"><span data-stu-id="fba1d-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="fba1d-129">Виртуальная сеть tooan канал ExpressRoute можно связать с помощью hello, выполнив командлет.</span><span class="sxs-lookup"><span data-stu-id="fba1d-129">You can link a virtual network tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="fba1d-130">Убедитесь, что шлюз виртуальной сети, hello создается и готов для связывания перед запуском командлета hello.</span><span class="sxs-lookup"><span data-stu-id="fba1d-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="fba1d-131">Подключить виртуальную сеть в цепи tooa другой подписке</span><span class="sxs-lookup"><span data-stu-id="fba1d-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="fba1d-132">Канал ExpressRoute может совместно использоваться несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="fba1d-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="fba1d-133">Следующий рисунок Hello показана простая схема способ управления доступом подходит для каналов ExpressRoute в нескольких подписках.</span><span class="sxs-lookup"><span data-stu-id="fba1d-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="fba1d-134">Каждый из hello маленькие облака в облако hello является используется toorepresent подписках, которые принадлежат toodifferent отделам в организации.</span><span class="sxs-lookup"><span data-stu-id="fba1d-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="fba1d-135">Каждого из отделов hello hello организации можно использовать собственную подписку для развертывания их службы — но hello отделы могут совместно использовать одной ExpressRoute цепи tooconnect tooyour назад в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="fba1d-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but hello departments can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="fba1d-136">Одному отделу (в этом примере: ИТ) может быть владельцем hello канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fba1d-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="fba1d-137">Другие подписки в hello организации можно использовать канал ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="fba1d-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="fba1d-138">Плата за подключение и пропускную способность для hello выделенного канала будет применен toohello владельца канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fba1d-138">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="fba1d-139">Все виртуальные сети совместно использовать hello же пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="fba1d-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Подключение между подписками](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="fba1d-141">Администрирование</span><span class="sxs-lookup"><span data-stu-id="fba1d-141">Administration</span></span>
<span data-ttu-id="fba1d-142">Hello *владельца канала* — администратор hello/coadministrator hello подписки, в которой hello ExpressRoute создан канал.</span><span class="sxs-lookup"><span data-stu-id="fba1d-142">hello *circuit owner* is hello administrator/coadministrator of hello subscription in which hello ExpressRoute circuit is created.</span></span> <span data-ttu-id="fba1d-143">Hello владелец канала может разрешить администраторам или coadministrators другие подписки, который ссылается tooas *circuit пользователей*, toouse hello выделенный канал, которой они владеют.</span><span class="sxs-lookup"><span data-stu-id="fba1d-143">hello circuit owner can authorize administrators/coadministrators of other subscriptions, referred tooas *circuit users*, toouse hello dedicated circuit that they own.</span></span> <span data-ttu-id="fba1d-144">Цепи пользователям, авторизованным toouse hello организации ExpressRoute канала может связать hello виртуальную сеть в своей подписки toohello канал ExpressRoute после прав.</span><span class="sxs-lookup"><span data-stu-id="fba1d-144">Circuit users who are authorized toouse hello organization's ExpressRoute circuit can link hello virtual network in their subscription toohello ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="fba1d-145">Владелец канала Hello имеет авторизаций toomodify и revoke power hello в любое время.</span><span class="sxs-lookup"><span data-stu-id="fba1d-145">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="fba1d-146">Отмена авторизации приведет к удалению из hello подписки, доступ к которым был отозван всех ссылок.</span><span class="sxs-lookup"><span data-stu-id="fba1d-146">Revoking an authorization will result in all links being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="fba1d-147">Действия владельца канала</span><span class="sxs-lookup"><span data-stu-id="fba1d-147">Circuit owner operations</span></span>

<span data-ttu-id="fba1d-148">**Создание разрешения**</span><span class="sxs-lookup"><span data-stu-id="fba1d-148">**Creating an authorization**</span></span>

<span data-ttu-id="fba1d-149">Hello владелец канала авторизует администраторов других подписок hello toouse hello указанного канала.</span><span class="sxs-lookup"><span data-stu-id="fba1d-149">hello circuit owner authorizes hello administrators of other subscriptions toouse hello specified circuit.</span></span> <span data-ttu-id="fba1d-150">В следующем примере hello Здравствуйте, администратор hello канала (ИТ компании Contoso) позволяет администратору hello из другой подписки (разработки тест) toolink копии схемы toohello tootwo виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="fba1d-150">In hello following example, hello administrator of hello circuit (Contoso IT) enables hello administrator of another subscription (Dev-Test) toolink up tootwo virtual networks toohello circuit.</span></span> <span data-ttu-id="fba1d-151">Здравствуйте, администратор Contoso ИТ данная возможность включена, указав идентификатор hello корпорации Майкрософт для разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="fba1d-151">hello Contoso IT administrator enables this by specifying hello Dev-Test Microsoft ID.</span></span> <span data-ttu-id="fba1d-152">командлет Hello не отправляет по электронной почте toohello указанный идентификатор Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="fba1d-152">hello cmdlet doesn't send email toohello specified Microsoft ID.</span></span> <span data-ttu-id="fba1d-153">Владелец канала Hello должен tooexplicitly уведомить hello другого владельца подписки, hello авторизации завершен.</span><span class="sxs-lookup"><span data-stu-id="fba1d-153">hello circuit owner needs tooexplicitly notify hello other subscription owner that hello authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="fba1d-154">**Просмотр разрешений**</span><span class="sxs-lookup"><span data-stu-id="fba1d-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="fba1d-155">Владелец канала Hello, можно просмотреть все разрешения, выданные для конкретного канала, выполнив следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="fba1d-155">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="fba1d-156">**Изменение разрешений**</span><span class="sxs-lookup"><span data-stu-id="fba1d-156">**Updating authorizations**</span></span>

<span data-ttu-id="fba1d-157">Владелец канала Hello можно изменить параметры авторизации с помощью hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="fba1d-157">hello circuit owner can modify authorizations by using hello following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="fba1d-158">**Удаление разрешений**</span><span class="sxs-lookup"><span data-stu-id="fba1d-158">**Deleting authorizations**</span></span>

<span data-ttu-id="fba1d-159">Владелец канала Hello можно revoke и удаление авторизации пользователя toohello, выполнив следующий командлет hello:</span><span class="sxs-lookup"><span data-stu-id="fba1d-159">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="fba1d-160">Действия пользователя канала</span><span class="sxs-lookup"><span data-stu-id="fba1d-160">Circuit user operations</span></span>

<span data-ttu-id="fba1d-161">**Просмотр разрешений**</span><span class="sxs-lookup"><span data-stu-id="fba1d-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="fba1d-162">Hello цепи пользователя можно просмотреть параметры авторизации с помощью hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="fba1d-162">hello circuit user can review authorizations by using hello following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="fba1d-163">**Активация разрешений на связь**</span><span class="sxs-lookup"><span data-stu-id="fba1d-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="fba1d-164">пользователя канала Hello можно выполнить следующий командлет tooredeem hello авторизации:</span><span class="sxs-lookup"><span data-stu-id="fba1d-164">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="fba1d-165">В подписке hello связаны вновь для hello виртуальной сети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fba1d-165">Run this command in hello newly linked subscription for hello virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="fba1d-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fba1d-166">Next steps</span></span>
<span data-ttu-id="fba1d-167">Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="fba1d-167">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

