---
title: "Связывание виртуальной сети tooan канал ExpressRoute: PowerShell: Azure | Документы Microsoft"
description: "Этот документ содержит общие сведения о том, как toolink виртуальных сетей (Vnet) tooExpressRoute каналов с помощью модели развертывания диспетчера ресурсов hello и PowerShell."
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
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="b9b5a-103">Подключение виртуальной сети tooan канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b9b5a-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b9b5a-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b9b5a-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="b9b5a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9b5a-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="b9b5a-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b9b5a-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="b9b5a-107">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="b9b5a-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="b9b5a-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="b9b5a-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="b9b5a-109">Эта статья поможет вам связать каналы ExpressRoute tooAzure виртуальных сетей (Vnet) с помощью модели развертывания диспетчера ресурсов hello и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="b9b5a-110">Виртуальные сети может быть либо в hello же часть другую подписку или подписку.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-110">Virtual networks can either be in hello same subscription or part of another subscription.</span></span> <span data-ttu-id="b9b5a-111">В этой статье также показано, как связать tooupdate виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-111">This article also shows you how tooupdate a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="b9b5a-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="b9b5a-112">Before you begin</span></span>
* <span data-ttu-id="b9b5a-113">Установите последнюю версию hello hello модули Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-113">Install hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="b9b5a-114">Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b9b5a-114">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="b9b5a-115">Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-115">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="b9b5a-116">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="b9b5a-117">Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-arm.md) и иметь цепи hello, предоставляемой поставщиком соединения.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-117">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="b9b5a-118">Убедитесь, что для вашего канала настроен частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="b9b5a-119">В разделе hello [Настройка маршрутизации](expressroute-howto-routing-arm.md) маршрутизации инструкции.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-119">See hello [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="b9b5a-120">Убедитесь, что настроен открытого пиринга Azure и hello пиринга BGP между вашей сетью и Майкрософт работает так, чтобы можно было включить подключение начала до конца.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-120">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="b9b5a-121">Вам необходимо создать и полностью подготовить виртуальную сеть и шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="b9b5a-122">Следуйте инструкциям hello слишком[создать шлюз виртуальной сети для ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b9b5a-122">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="b9b5a-123">Шлюз виртуальной сети для ExpressRoute использует hello «ExpressRoute», тип шлюза не VPN.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-123">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="b9b5a-124">Объедините too10 виртуальных сетей tooa стандартные каналом expressroute.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-124">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="b9b5a-125">Все виртуальные сети должны быть в hello геополитические совпадают при использовании стандартных канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-125">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="b9b5a-126">Можно связать виртуальных сетей за пределами области геополитические hello объекта hello канал ExpressRoute или подключения большее количество виртуальных сетей tooyour канал ExpressRoute, если вы включили hello ExpressRoute премиальное дополнение.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-126">You can link a virtual networks outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="b9b5a-127">Проверьте hello [часто задаваемые вопросы о](expressroute-faqs.md) Дополнительные сведения о премиальное дополнение hello.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="b9b5a-128">Подключить виртуальную сеть в Привет одному каналу tooa подписки</span><span class="sxs-lookup"><span data-stu-id="b9b5a-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="b9b5a-129">Tooan шлюза виртуальной сети канал ExpressRoute можно подключиться с помощью hello, выполнив командлет.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-129">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="b9b5a-130">Убедитесь, что шлюз виртуальной сети, hello создается и готов для связывания перед запуском командлета hello:</span><span class="sxs-lookup"><span data-stu-id="b9b5a-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="b9b5a-131">Подключить виртуальную сеть в цепи tooa другой подписке</span><span class="sxs-lookup"><span data-stu-id="b9b5a-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="b9b5a-132">Канал ExpressRoute может совместно использоваться несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="b9b5a-133">Следующий рисунок Hello показана простая схема способ управления доступом подходит для каналов ExpressRoute в нескольких подписках.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="b9b5a-134">Каждый из hello маленькие облака в облако hello является используется toorepresent подписках, которые принадлежат toodifferent отделам в организации.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="b9b5a-135">Каждый из отделов hello hello организации можно использовать собственную подписку для развертывания своих служб--, но они могут совместно использовать одной ExpressRoute цепи tooconnect tooyour назад в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="b9b5a-136">Одному отделу (в этом примере: ИТ) может быть владельцем hello канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="b9b5a-137">Другие подписки в hello организации можно использовать канал ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="b9b5a-138">Плата за подключение и пропускную способность для hello канал ExpressRoute будет применен toohello владельца подписки.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-138">Connectivity and bandwidth charges for hello ExpressRoute circuit will be applied toohello subscription owner.</span></span> <span data-ttu-id="b9b5a-139">Все виртуальные сети совместно использовать hello же пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Подключение между подписками](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="b9b5a-141">Администрирование: владельцы канала и его пользователи</span><span class="sxs-lookup"><span data-stu-id="b9b5a-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="b9b5a-142">Hello «владелец схемы» зарегистрирован как авторизованный пользователь питания, для hello ресурсов цепь ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-142">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="b9b5a-143">Владелец канала Hello можно создать авторизацию, может быть активирован с «канала пользователи».</span><span class="sxs-lookup"><span data-stu-id="b9b5a-143">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="b9b5a-144">Пользователи канала являются владельцами виртуальной сети hello шлюзов, которые не находятся в одной подписке, как hello канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-144">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="b9b5a-145">Пользователи канала могут активировать разрешения (по одному разрешению для каждой виртуальной сети).</span><span class="sxs-lookup"><span data-stu-id="b9b5a-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="b9b5a-146">Владелец канала Hello имеет авторизаций toomodify и revoke power hello в любое время.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-146">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="b9b5a-147">Отмена авторизации приведет все подключения ссылку, удаляемый из подписки hello, доступ к которым был отозван.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-147">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="b9b5a-148">Действия владельца канала</span><span class="sxs-lookup"><span data-stu-id="b9b5a-148">Circuit owner operations</span></span>

<span data-ttu-id="b9b5a-149">**toocreate авторизации**</span><span class="sxs-lookup"><span data-stu-id="b9b5a-149">**toocreate an authorization**</span></span>

<span data-ttu-id="b9b5a-150">Владелец канала Hello создает авторизации.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-150">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="b9b5a-151">Это приведет к создание hello ключ авторизации, которое может быть используемые схемы пользователя tooconnect их toohello шлюзы виртуальной сети канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-151">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="b9b5a-152">Разрешение действительно только для одного подключения.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="b9b5a-153">Hello в следующем фрагменте кода показан командлет как toocreate авторизации:</span><span class="sxs-lookup"><span data-stu-id="b9b5a-153">hello following cmdlet snippet shows how toocreate an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="b9b5a-154">Hello toothis ответ будет содержать ключ авторизации hello и состояние:</span><span class="sxs-lookup"><span data-stu-id="b9b5a-154">hello response toothis will contain hello authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="b9b5a-155">**tooreview авторизации**</span><span class="sxs-lookup"><span data-stu-id="b9b5a-155">**tooreview authorizations**</span></span>

<span data-ttu-id="b9b5a-156">Владелец канала Hello, можно просмотреть все разрешения, выданные для конкретного канала, выполнив следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-156">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="b9b5a-157">**tooadd авторизации**</span><span class="sxs-lookup"><span data-stu-id="b9b5a-157">**tooadd authorizations**</span></span>

<span data-ttu-id="b9b5a-158">Владелец канала Hello можно добавить параметры авторизации с помощью hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="b9b5a-158">hello circuit owner can add authorizations by using hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="b9b5a-159">**toodelete авторизации**</span><span class="sxs-lookup"><span data-stu-id="b9b5a-159">**toodelete authorizations**</span></span>

<span data-ttu-id="b9b5a-160">Владелец канала Hello можно revoke и удаление авторизации пользователя toohello, выполнив следующий командлет hello:</span><span class="sxs-lookup"><span data-stu-id="b9b5a-160">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="b9b5a-161">Действия пользователя канала</span><span class="sxs-lookup"><span data-stu-id="b9b5a-161">Circuit user operations</span></span>

<span data-ttu-id="b9b5a-162">пользователь канала Hello должен идентификатор однорангового hello и ключ авторизации от владельца канала hello.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-162">hello circuit user needs hello peer ID and an authorization key from hello circuit owner.</span></span> <span data-ttu-id="b9b5a-163">ключ авторизации Hello представляет собой идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-163">hello authorization key is a GUID.</span></span>

<span data-ttu-id="b9b5a-164">Идентификатор однорангового узла можно проверить из hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b9b5a-164">Peer ID can be checked from hello following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="b9b5a-165">**tooredeem авторизации подключения**</span><span class="sxs-lookup"><span data-stu-id="b9b5a-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="b9b5a-166">пользователя канала Hello можно выполнить следующий командлет tooredeem hello авторизации:</span><span class="sxs-lookup"><span data-stu-id="b9b5a-166">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="b9b5a-167">**toorelease авторизации подключения**</span><span class="sxs-lookup"><span data-stu-id="b9b5a-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="b9b5a-168">Авторизации можно освободить путем удаления соединений hello, связывающий hello цепь ExpressRoute toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="b9b5a-169">Изменение подключения к виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="b9b5a-169">Modify a virtual network connection</span></span>
<span data-ttu-id="b9b5a-170">Вы можете изменить определенные свойства подключения к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="b9b5a-171">**Вес подключения tooupdate hello**</span><span class="sxs-lookup"><span data-stu-id="b9b5a-171">**tooupdate hello connection weight**</span></span>

<span data-ttu-id="b9b5a-172">Виртуальная сеть может быть подключенных toomultiple каналы ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-172">Your virtual network can be connected toomultiple ExpressRoute circuits.</span></span> <span data-ttu-id="b9b5a-173">Может появиться hello одинаковые префиксы из более чем один канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-173">You may receive hello same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="b9b5a-174">toochoose, какой трафик toosend подключения, предназначенные для этого префикса, вы можете изменить *недопустимо* соединения.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-174">toochoose which connection toosend traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="b9b5a-175">Трафик будет отправляться по соединению, hello с наивысшим hello *недопустимо*.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-175">Traffic will be sent on hello connection with hello highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="b9b5a-176">Здравствуйте, диапазон *недопустимо* — 0 too32000.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-176">hello range of *RoutingWeight* is 0 too32000.</span></span> <span data-ttu-id="b9b5a-177">значение по умолчанию Hello — 0.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-177">hello default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9b5a-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9b5a-178">Next steps</span></span>
<span data-ttu-id="b9b5a-179">Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="b9b5a-179">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
