---
title: "Связывание виртуальной сети с каналом ExpressRoute с помощью PowerShell и Azure | Документация Майкрософт"
description: "В этом документе содержатся общие сведения о связывании виртуальных сетей с каналами ExpressRoute с помощью модели развертывания Resource Manager и PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: 8c2f3036f754a98090ab860f95900416690ebf83
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="66ba0-103">Подключение виртуальной сети к каналу ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="66ba0-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="66ba0-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="66ba0-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="66ba0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="66ba0-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="66ba0-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="66ba0-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="66ba0-107">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="66ba0-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="66ba0-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="66ba0-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="66ba0-109">Эта статья поможет вам связать виртуальные сети с каналами Azure ExpressRoute с помощью модели развертывания Resource Manager и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66ba0-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="66ba0-110">Виртуальные сети могут входить в одну и ту же подписку или в разные подписки.</span><span class="sxs-lookup"><span data-stu-id="66ba0-110">Virtual networks can either be in the same subscription or part of another subscription.</span></span> <span data-ttu-id="66ba0-111">В этой статье также показано, как обновить связь виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="66ba0-111">This article also shows you how to update a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="66ba0-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="66ba0-112">Before you begin</span></span>
* <span data-ttu-id="66ba0-113">Установите последние версии модулей Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66ba0-113">Install the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="66ba0-114">Дополнительные сведения см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="66ba0-114">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="66ba0-115">Прежде чем приступить к настройке, изучите [предварительные требования](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md) и [рабочие процессы](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="66ba0-115">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="66ba0-116">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="66ba0-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="66ba0-117">Следуйте инструкциям, чтобы [создать канал ExpressRoute](expressroute-howto-circuit-arm.md) и включить его на стороне поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="66ba0-117">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="66ba0-118">Убедитесь, что для вашего канала настроен частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="66ba0-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="66ba0-119">Инструкции по маршрутизации см. в статье [Настройка маршрутизации](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="66ba0-119">See the [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="66ba0-120">Для создания сквозного подключения обязательно настройте частный пиринг Azure, а также пиринг BGP между вашей сетью и сетью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="66ba0-120">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="66ba0-121">Вам необходимо создать и полностью подготовить виртуальную сеть и шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="66ba0-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="66ba0-122">Следуйте инструкциям по [созданию шлюза виртуальной сети для ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="66ba0-122">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="66ba0-123">Для ExpressRoute используется шлюз виртуальной сети типа ExpressRoute, а не VPN.</span><span class="sxs-lookup"><span data-stu-id="66ba0-123">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="66ba0-124">К стандартному каналу ExpressRoute можно подключить не более 10 виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="66ba0-124">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="66ba0-125">Если используется стандартный канал ExpressRoute, все виртуальные сети должны находиться в одном геополитическом регионе.</span><span class="sxs-lookup"><span data-stu-id="66ba0-125">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="66ba0-126">Если включить надстройку ExpressRoute Premium, вы сможете подключить к каналу ExpressRoute больше виртуальных сетей, включая сети из других геополитических регионов.</span><span class="sxs-lookup"><span data-stu-id="66ba0-126">You can link a virtual networks outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="66ba0-127">Дополнительную информацию о надстройке Premium см. в разделе [Вопросы и ответы](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="66ba0-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="66ba0-128">Подключение к каналу виртуальной сети в той же подписке</span><span class="sxs-lookup"><span data-stu-id="66ba0-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="66ba0-129">Вы можете связать шлюз виртуальной сети с каналом ExpressRoute, используя следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="66ba0-129">You can connect a virtual network gateway to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="66ba0-130">Убедитесь в наличии шлюза виртуальной сети и его готовности к связыванию, прежде чем выполнять командлет.</span><span class="sxs-lookup"><span data-stu-id="66ba0-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="66ba0-131">Подключение к каналу виртуальной сети в другой подписке</span><span class="sxs-lookup"><span data-stu-id="66ba0-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="66ba0-132">Канал ExpressRoute может совместно использоваться несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="66ba0-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="66ba0-133">На рисунке ниже схематично показан способ совместного использования каналов ExpressRoute несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="66ba0-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="66ba0-134">Каждое маленькое облако внутри большого облака представляет подписки, принадлежащие различным подразделениям одной организации.</span><span class="sxs-lookup"><span data-stu-id="66ba0-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="66ba0-135">Любое подразделение в организации может использовать свою собственную подписку для развертывания служб. Кроме того, оно может совместно использовать один выделенный канал ExpressRoute для подключения к корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="66ba0-135">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="66ba0-136">Владельцем канала ExpressRoute может выступать одно подразделение (в данном примере — ИТ-подразделение).</span><span class="sxs-lookup"><span data-stu-id="66ba0-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="66ba0-137">Другие подписки в организации могут использовать канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="66ba0-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="66ba0-138">Плата за подключение канала ExpressRoute и использование полосы пропускания будет взиматься с владельца подписки.</span><span class="sxs-lookup"><span data-stu-id="66ba0-138">Connectivity and bandwidth charges for the ExpressRoute circuit will be applied to the subscription owner.</span></span> <span data-ttu-id="66ba0-139">Полоса пропускания распределяется между всеми виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="66ba0-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Подключение между подписками](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="66ba0-141">Администрирование: владельцы канала и его пользователи</span><span class="sxs-lookup"><span data-stu-id="66ba0-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="66ba0-142">Владельцем канала является уполномоченный опытный пользователь ресурса канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="66ba0-142">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="66ba0-143">Владелец канала может создавать разрешения, которые могут быть активированы пользователями канала.</span><span class="sxs-lookup"><span data-stu-id="66ba0-143">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="66ba0-144">Пользователи канала являются владельцами шлюзов виртуальных сетей (которые находятся в разных подписках с каналом ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="66ba0-144">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="66ba0-145">Пользователи канала могут активировать разрешения (по одному разрешению для каждой виртуальной сети).</span><span class="sxs-lookup"><span data-stu-id="66ba0-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="66ba0-146">Владелец канала имеет право изменить или отменить авторизацию в любое время.</span><span class="sxs-lookup"><span data-stu-id="66ba0-146">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="66ba0-147">Отмена разрешения приводит к удалению всех связывающих подключений из подписки, доступ к которой был отменен.</span><span class="sxs-lookup"><span data-stu-id="66ba0-147">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="66ba0-148">Действия владельца канала</span><span class="sxs-lookup"><span data-stu-id="66ba0-148">Circuit owner operations</span></span>

<span data-ttu-id="66ba0-149">**Создание разрешения**</span><span class="sxs-lookup"><span data-stu-id="66ba0-149">**To create an authorization**</span></span>

<span data-ttu-id="66ba0-150">Владелец канала создает разрешение.</span><span class="sxs-lookup"><span data-stu-id="66ba0-150">The circuit owner creates an authorization.</span></span> <span data-ttu-id="66ba0-151">Это приводит к созданию ключа разрешения, который может использоваться пользователем канала для подключения шлюзов виртуальной сети к каналу ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="66ba0-151">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="66ba0-152">Разрешение действительно только для одного подключения.</span><span class="sxs-lookup"><span data-stu-id="66ba0-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="66ba0-153">В следующем фрагменте показано создание разрешения с помощью командлета.</span><span class="sxs-lookup"><span data-stu-id="66ba0-153">The following cmdlet snippet shows how to create an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="66ba0-154">Ответ будет содержать ключ и состояние разрешения.</span><span class="sxs-lookup"><span data-stu-id="66ba0-154">The response to this will contain the authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="66ba0-155">**Просмотр разрешений**</span><span class="sxs-lookup"><span data-stu-id="66ba0-155">**To review authorizations**</span></span>

<span data-ttu-id="66ba0-156">Владелец канала может просмотреть все разрешения, выданные для определенного канала, выполнив следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="66ba0-156">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="66ba0-157">**Добавление разрешений**</span><span class="sxs-lookup"><span data-stu-id="66ba0-157">**To add authorizations**</span></span>

<span data-ttu-id="66ba0-158">Владелец канала может добавлять разрешения с помощью следующего командлета.</span><span class="sxs-lookup"><span data-stu-id="66ba0-158">The circuit owner can add authorizations by using the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="66ba0-159">**Удаление разрешений**</span><span class="sxs-lookup"><span data-stu-id="66ba0-159">**To delete authorizations**</span></span>

<span data-ttu-id="66ba0-160">Владелец канала может отзывать (удалять) разрешения, выданные пользователю, с помощью следующего командлета.</span><span class="sxs-lookup"><span data-stu-id="66ba0-160">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="66ba0-161">Действия пользователя канала</span><span class="sxs-lookup"><span data-stu-id="66ba0-161">Circuit user operations</span></span>

<span data-ttu-id="66ba0-162">Пользователь канала должен получить от владельца канала идентификатор однорангового узла и ключ разрешения.</span><span class="sxs-lookup"><span data-stu-id="66ba0-162">The circuit user needs the peer ID and an authorization key from the circuit owner.</span></span> <span data-ttu-id="66ba0-163">Ключ разрешения представляет собой идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="66ba0-163">The authorization key is a GUID.</span></span>

<span data-ttu-id="66ba0-164">Идентификатор однорангового узла можно проверить с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="66ba0-164">Peer ID can be checked from the following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="66ba0-165">**Активация разрешения на подключение**</span><span class="sxs-lookup"><span data-stu-id="66ba0-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="66ba0-166">Пользователь канала может активировать разрешение на связь, выполнив следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="66ba0-166">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="66ba0-167">**Освобождение разрешения на подключение**</span><span class="sxs-lookup"><span data-stu-id="66ba0-167">**To release a connection authorization**</span></span>

<span data-ttu-id="66ba0-168">Разрешение можно освободить, удалив подключение, связывающее канал ExpressRoute и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="66ba0-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="66ba0-169">Изменение подключения к виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="66ba0-169">Modify a virtual network connection</span></span>
<span data-ttu-id="66ba0-170">Вы можете изменить определенные свойства подключения к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="66ba0-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="66ba0-171">**Изменение веса подключения**</span><span class="sxs-lookup"><span data-stu-id="66ba0-171">**To update the connection weight**</span></span>

<span data-ttu-id="66ba0-172">Виртуальная сеть может подключаться к нескольким каналам ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="66ba0-172">Your virtual network can be connected to multiple ExpressRoute circuits.</span></span> <span data-ttu-id="66ba0-173">Одинаковый префикс может быть получен из нескольких каналов ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="66ba0-173">You may receive the same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="66ba0-174">Чтобы выбрать подключение для отправки трафика, предназначенного для этого префикса, можно изменить значение *RoutingWeight* подключения.</span><span class="sxs-lookup"><span data-stu-id="66ba0-174">To choose which connection to send traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="66ba0-175">Трафик будет отправляться через подключение с самым высоким значением *RoutingWeight*.</span><span class="sxs-lookup"><span data-stu-id="66ba0-175">Traffic will be sent on the connection with the highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="66ba0-176">Диапазон значений *RoutingWeight*: 0 до 32 000.</span><span class="sxs-lookup"><span data-stu-id="66ba0-176">The range of *RoutingWeight* is 0 to 32000.</span></span> <span data-ttu-id="66ba0-177">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="66ba0-177">The default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66ba0-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66ba0-178">Next steps</span></span>
<span data-ttu-id="66ba0-179">Дополнительные сведения об ExpressRoute см. в статье [Вопросы и ответы по ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="66ba0-179">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
