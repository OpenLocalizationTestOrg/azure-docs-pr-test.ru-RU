---
title: "Связывание виртуальной сети с каналом ExpressRoute с помощью PowerShell и классического портала Azure | Документация Майкрософт"
description: "В этом документе содержатся общие сведения о связывании виртуальных сетей с каналами ExpressRoute с помощью классической модели развертывания и PowerShell."
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
ms.openlocfilehash: 8df8a4c6ff0897c821e13248e0494b17e1a4992d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="f330b-103">Подключение виртуальной сети к каналу ExpressRoute с помощью PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="f330b-103">Connect a virtual network to an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f330b-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="f330b-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="f330b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f330b-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="f330b-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="f330b-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="f330b-107">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="f330b-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="f330b-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="f330b-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="f330b-109">В этой статье содержатся сведения о связывании виртуальных сетей с каналами Azure ExpressRoute с помощью классической модели развертывания и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f330b-109">This article will help you link virtual networks (VNets) to Azure ExpressRoute circuits by using the classic deployment model and PowerShell.</span></span> <span data-ttu-id="f330b-110">Виртуальные сети могут быть в той же или другой подписке.</span><span class="sxs-lookup"><span data-stu-id="f330b-110">Virtual networks can either be in the same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="f330b-111">**О моделях развертывания Azure**</span><span class="sxs-lookup"><span data-stu-id="f330b-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="f330b-112">Предварительные требования для настройки</span><span class="sxs-lookup"><span data-stu-id="f330b-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="f330b-113">Нужна последняя версия модулей Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f330b-113">You need the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="f330b-114">Последнюю версию модулей PowerShell можно скачать из раздела PowerShell на [странице скачивания Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f330b-114">You can download the latest PowerShell modules from the PowerShell section of the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="f330b-115">Пошаговые инструкции по настройке компьютера для использования модулей Azure PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f330b-115">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>
2. <span data-ttu-id="f330b-116">Прежде чем приступить к настройке, необходимо изучить [предварительные требования](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md) и [рабочие процессы](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="f330b-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="f330b-117">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f330b-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="f330b-118">Следуйте инструкциям, чтобы [создать канал ExpressRoute](expressroute-howto-circuit-classic.md) и включить его на стороне поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="f330b-118">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable the circuit.</span></span>
   * <span data-ttu-id="f330b-119">Убедитесь, что для вашего канала настроен частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="f330b-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="f330b-120">Инструкции по маршрутизации см. в статье [Настройка маршрутизации](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="f330b-120">See the [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="f330b-121">Для создания сквозного подключения обязательно настройте частный пиринг Azure, а также пиринг BGP между вашей сетью и сетью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f330b-121">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="f330b-122">Вам необходимо иметь созданные и полностью подготовленные виртуальную сеть и шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f330b-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="f330b-123">Следуйте инструкциям по [настройке виртуальной сети для ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="f330b-123">Follow the instructions to [configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="f330b-124">Вы можете связать с каналом ExpressRoute до 10 виртуальных сетей включительно.</span><span class="sxs-lookup"><span data-stu-id="f330b-124">You can link up to 10 virtual networks to an ExpressRoute circuit.</span></span> <span data-ttu-id="f330b-125">Все виртуальные машины должны находиться в одном геополитическом регионе.</span><span class="sxs-lookup"><span data-stu-id="f330b-125">All virtual networks must be in the same geopolitical region.</span></span> <span data-ttu-id="f330b-126">При использовании надстройки Premium вы сможете связать больше виртуальных сетей с каналом ExpressRoute или связать виртуальные сети, которые находятся в других геополитических регионах.</span><span class="sxs-lookup"><span data-stu-id="f330b-126">You can link a larger number of virtual networks to your ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="f330b-127">Дополнительную информацию о надстройке Premium см. в разделе [Вопросы и ответы](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="f330b-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="f330b-128">Подключение к каналу виртуальной сети в той же подписке</span><span class="sxs-lookup"><span data-stu-id="f330b-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="f330b-129">Вы можете связать виртуальную сеть с каналом ExpressRoute, используя следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="f330b-129">You can link a virtual network to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="f330b-130">Убедитесь в наличии шлюза виртуальной сети и его готовности к связыванию, прежде чем запускать командлет.</span><span class="sxs-lookup"><span data-stu-id="f330b-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="f330b-131">Подключение к каналу виртуальной сети в другой подписке</span><span class="sxs-lookup"><span data-stu-id="f330b-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="f330b-132">Канал ExpressRoute может совместно использоваться несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="f330b-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="f330b-133">На рисунке ниже схематично показан способ совместного использования каналов ExpressRoute несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="f330b-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="f330b-134">Каждое маленькое облако внутри большого облака представляет подписки, принадлежащие различным подразделениям одной организации.</span><span class="sxs-lookup"><span data-stu-id="f330b-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="f330b-135">Любое подразделение в организации может использовать свою собственную подписку для развертывания своих служб. Кроме того, подразделения могут совместно использовать один выделенный канал ExpressRoute для подключения к корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="f330b-135">Each of the departments within the organization can use their own subscription for deploying their services--but the departments can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="f330b-136">Владельцем канала ExpressRoute может выступать одно подразделение (в данном примере — ИТ-подразделение).</span><span class="sxs-lookup"><span data-stu-id="f330b-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="f330b-137">Другие подписки в организации могут использовать канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f330b-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="f330b-138">Плата за подключение выделенного канала ExpressRoute и использование полосы пропускания будет взиматься с владельца выделенного канала.</span><span class="sxs-lookup"><span data-stu-id="f330b-138">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="f330b-139">Полоса пропускания распределяется между всеми виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="f330b-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Подключение между подписками](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="f330b-141">Администрирование</span><span class="sxs-lookup"><span data-stu-id="f330b-141">Administration</span></span>
<span data-ttu-id="f330b-142">*Владелец канала* — это администратор или соадминистратор подписки, в которой создан канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f330b-142">The *circuit owner* is the administrator/coadministrator of the subscription in which the ExpressRoute circuit is created.</span></span> <span data-ttu-id="f330b-143">Владелец канала может разрешить использовать свой выделенный канал администраторам и соадминистраторам других подписок (на схеме рабочего процесса они называются *пользователями канала*).</span><span class="sxs-lookup"><span data-stu-id="f330b-143">The circuit owner can authorize administrators/coadministrators of other subscriptions, referred to as *circuit users*, to use the dedicated circuit that they own.</span></span> <span data-ttu-id="f330b-144">Пользователи, получившие разрешение на использование канала ExpressRoute организации, смогут связать виртуальную сеть в своей подписке с этим каналом ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f330b-144">Circuit users who are authorized to use the organization's ExpressRoute circuit can link the virtual network in their subscription to the ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="f330b-145">Владелец канала имеет право изменить или отменить авторизацию в любое время.</span><span class="sxs-lookup"><span data-stu-id="f330b-145">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="f330b-146">Отмена авторизации приводит к удалению всех ссылок из подписки, доступ которой был отменен.</span><span class="sxs-lookup"><span data-stu-id="f330b-146">Revoking an authorization will result in all links being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="f330b-147">Действия владельца канала</span><span class="sxs-lookup"><span data-stu-id="f330b-147">Circuit owner operations</span></span>

<span data-ttu-id="f330b-148">**Создание разрешения**</span><span class="sxs-lookup"><span data-stu-id="f330b-148">**Creating an authorization**</span></span>

<span data-ttu-id="f330b-149">Владелец канала разрешает администраторам других подписок использовать указанный канал.</span><span class="sxs-lookup"><span data-stu-id="f330b-149">The circuit owner authorizes the administrators of other subscriptions to use the specified circuit.</span></span> <span data-ttu-id="f330b-150">В приведенном ниже примере администратор канала (Contoso IT) разрешает администратору другой подписки (Dev-Test) привязать к этому каналу две виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="f330b-150">In the following example, the administrator of the circuit (Contoso IT) enables the administrator of another subscription (Dev-Test) to link up to two virtual networks to the circuit.</span></span> <span data-ttu-id="f330b-151">Администратор Contoso IT разрешает это, указав идентификатор Майкрософт подписки Dev-Test.</span><span class="sxs-lookup"><span data-stu-id="f330b-151">The Contoso IT administrator enables this by specifying the Dev-Test Microsoft ID.</span></span> <span data-ttu-id="f330b-152">Командлет не отправляет по электронной почте указанный идентификатор Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f330b-152">The cmdlet doesn't send email to the specified Microsoft ID.</span></span> <span data-ttu-id="f330b-153">Владелец канала должен сам уведомить владельца другой подписки о том, что авторизация завершена.</span><span class="sxs-lookup"><span data-stu-id="f330b-153">The circuit owner needs to explicitly notify the other subscription owner that the authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="f330b-154">**Просмотр разрешений**</span><span class="sxs-lookup"><span data-stu-id="f330b-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="f330b-155">Владелец канала может просмотреть все разрешения, выданные для определенного канала, выполнив следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="f330b-155">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

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


<span data-ttu-id="f330b-156">**Изменение разрешений**</span><span class="sxs-lookup"><span data-stu-id="f330b-156">**Updating authorizations**</span></span>

<span data-ttu-id="f330b-157">Владелец канала может изменять разрешения с помощью следующего командлета.</span><span class="sxs-lookup"><span data-stu-id="f330b-157">The circuit owner can modify authorizations by using the following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="f330b-158">**Удаление разрешений**</span><span class="sxs-lookup"><span data-stu-id="f330b-158">**Deleting authorizations**</span></span>

<span data-ttu-id="f330b-159">Владелец канала может отзывать (удалять) разрешения, выданные пользователю, с помощью следующего командлета.</span><span class="sxs-lookup"><span data-stu-id="f330b-159">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="f330b-160">Действия пользователя канала</span><span class="sxs-lookup"><span data-stu-id="f330b-160">Circuit user operations</span></span>

<span data-ttu-id="f330b-161">**Просмотр разрешений**</span><span class="sxs-lookup"><span data-stu-id="f330b-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="f330b-162">Пользователь канала может просматривать разрешения с помощью следующего командлета.</span><span class="sxs-lookup"><span data-stu-id="f330b-162">The circuit user can review authorizations by using the following cmdlet:</span></span>

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

<span data-ttu-id="f330b-163">**Активация разрешений на связь**</span><span class="sxs-lookup"><span data-stu-id="f330b-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="f330b-164">Пользователь канала может активировать разрешение на связь, выполнив следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="f330b-164">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="f330b-165">Выполните следующую команду в только что связанной подписке для виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="f330b-165">Run this command in the newly linked subscription for the virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="f330b-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f330b-166">Next steps</span></span>
<span data-ttu-id="f330b-167">Дополнительные сведения об ExpressRoute см. в статье [Вопросы и ответы по ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="f330b-167">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

