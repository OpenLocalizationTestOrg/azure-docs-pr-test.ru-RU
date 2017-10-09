---
title: "Связывание виртуальной сети tooan канал ExpressRoute: CLI: Azure | Документы Microsoft"
description: "Этот документ содержит общие сведения о том, как toolink виртуальных сетей (Vnet) tooExpressRoute каналов с помощью модели развертывания диспетчера ресурсов hello и интерфейс командной строки."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a><span data-ttu-id="4994c-103">Подключение с использованием интерфейса CLI канал ExpressRoute tooan виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="4994c-103">Connect a virtual network tooan ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="4994c-104">Эта статья поможет вам ссылку с помощью CLI каналы ExpressRoute tooAzure виртуальных сетей (Vnet).</span><span class="sxs-lookup"><span data-stu-id="4994c-104">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="4994c-105">с помощью Azure CLI toolink hello виртуальные сети должны создаваться с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="4994c-105">toolink using Azure CLI, hello virtual networks must be created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="4994c-106">Они могут быть либо в hello одной подписке или входить в другую подписку.</span><span class="sxs-lookup"><span data-stu-id="4994c-106">They can either be in hello same subscription, or part of another subscription.</span></span> <span data-ttu-id="4994c-107">Если вы хотите toouse tooconnect другой метод вашей виртуальной сети tooan канал ExpressRoute, можно выбрать статьи из hello после списка:</span><span class="sxs-lookup"><span data-stu-id="4994c-107">If you want toouse a different method tooconnect your VNet tooan ExpressRoute circuit, you can select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4994c-108">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="4994c-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="4994c-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4994c-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="4994c-110">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="4994c-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="4994c-111">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="4994c-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="4994c-112">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="4994c-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="4994c-113">Предварительные требования для настройки</span><span class="sxs-lookup"><span data-stu-id="4994c-113">Configuration prerequisites</span></span>

* <span data-ttu-id="4994c-114">Требуется последняя версия hello hello командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="4994c-114">You need hello latest version of hello command-line interface (CLI).</span></span> <span data-ttu-id="4994c-115">Дополнительные сведения см. в статье [Установка Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4994c-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="4994c-116">Требуется tooreview hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="4994c-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="4994c-117">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4994c-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="4994c-118">Следуйте инструкциям hello слишком[создать канал ExpressRoute](howto-circuit-cli.md) и иметь цепи hello, предоставляемой поставщиком соединения.</span><span class="sxs-lookup"><span data-stu-id="4994c-118">Follow hello instructions too[create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="4994c-119">Убедитесь, что для вашего канала настроен частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="4994c-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="4994c-120">В разделе hello [Настройка маршрутизации](howto-routing-cli.md) маршрутизации инструкции.</span><span class="sxs-lookup"><span data-stu-id="4994c-120">See hello [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="4994c-121">Убедитесь, что настроен частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="4994c-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="4994c-122">Hello пиринга BGP между вашей сетью и Майкрософт должны работать так, чтобы можно было включить подключение начала до конца.</span><span class="sxs-lookup"><span data-stu-id="4994c-122">hello BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="4994c-123">Вам необходимо создать и полностью подготовить виртуальную сеть и шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="4994c-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="4994c-124">Следуйте инструкциям hello слишком[настроить шлюз виртуальной сети для ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="4994c-124">Follow hello instructions too[Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="4994c-125">Быть убедиться, что toouse `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="4994c-125">Be sure toouse `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="4994c-126">Объедините too10 виртуальных сетей tooa стандартные каналом expressroute.</span><span class="sxs-lookup"><span data-stu-id="4994c-126">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="4994c-127">Все виртуальные сети должны быть в hello геополитические совпадают при использовании стандартных канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4994c-127">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="4994c-128">При включении hello ExpressRoute премиальное дополнение можно связать виртуальную сеть за пределами области геополитические hello объекта hello канал ExpressRoute или подключения большее количество виртуальных сетей tooyour канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4994c-128">If you enable hello ExpressRoute premium add-on, you can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="4994c-129">Дополнительные сведения о премиальное дополнение hello. в разделе hello [часто задаваемые вопросы о](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="4994c-129">For more information about hello premium add-on, see hello [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="4994c-130">Подключить виртуальную сеть в Привет одному каналу tooa подписки</span><span class="sxs-lookup"><span data-stu-id="4994c-130">Connect a virtual network in hello same subscription tooa circuit</span></span>

<span data-ttu-id="4994c-131">Канал ExpressRoute tooan шлюза виртуальной сети можно подключиться, используя пример hello.</span><span class="sxs-lookup"><span data-stu-id="4994c-131">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello example.</span></span> <span data-ttu-id="4994c-132">Убедитесь, что шлюз виртуальной сети, hello создается и готов для связывания перед выполнением команды hello.</span><span class="sxs-lookup"><span data-stu-id="4994c-132">Make sure that hello virtual network gateway is created and is ready for linking before you run hello command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="4994c-133">Подключить виртуальную сеть в цепи tooa другой подписке</span><span class="sxs-lookup"><span data-stu-id="4994c-133">Connect a virtual network in a different subscription tooa circuit</span></span>

<span data-ttu-id="4994c-134">Канал ExpressRoute может совместно использоваться несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="4994c-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="4994c-135">на следующем рисунке Hello показана простая схема способ управления доступом подходит для каналов ExpressRoute в нескольких подписках.</span><span class="sxs-lookup"><span data-stu-id="4994c-135">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="4994c-136">Каждый из hello маленькие облака в облако hello является используется toorepresent подписках, которые принадлежат toodifferent отделам в организации.</span><span class="sxs-lookup"><span data-stu-id="4994c-136">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="4994c-137">Каждый из отделов hello hello организации можно использовать собственную подписку для развертывания своих служб--, но они могут совместно использовать одной ExpressRoute цепи tooconnect tooyour назад в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="4994c-137">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="4994c-138">Одному отделу (в этом примере: ИТ) может быть владельцем hello канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4994c-138">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="4994c-139">Другие подписки в hello организации можно использовать канал ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="4994c-139">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="4994c-140">Плата за подключение и пропускную способность для hello выделенного канала будет применен toohello владельца канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4994c-140">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="4994c-141">Все виртуальные сети совместно использовать hello же пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="4994c-141">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Подключение между подписками](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="4994c-143">Администрирование: владельцы и пользователи канала</span><span class="sxs-lookup"><span data-stu-id="4994c-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="4994c-144">Hello «Владелец схемы» зарегистрирован как авторизованный пользователь питания, для hello ресурсов цепь ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4994c-144">hello 'Circuit Owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="4994c-145">Hello владельца канала можно создать авторизацию, может быть активирован с «Канала пользователи».</span><span class="sxs-lookup"><span data-stu-id="4994c-145">hello Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="4994c-146">Пользователи канала являются владельцами виртуальной сети hello шлюзов, которые не находятся в одной подписке, как hello канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4994c-146">Circuit Users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="4994c-147">Пользователи канала могут использовать разрешения (по одному разрешению на виртуальную сеть).</span><span class="sxs-lookup"><span data-stu-id="4994c-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="4994c-148">Hello владельца канала имеет авторизаций toomodify и revoke power hello в любое время.</span><span class="sxs-lookup"><span data-stu-id="4994c-148">hello Circuit Owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="4994c-149">При отзыве авторизации все связи соединения удаляются из подписки hello, доступ к которым был отозван.</span><span class="sxs-lookup"><span data-stu-id="4994c-149">When an authorization is revoked, all link connections are deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="4994c-150">Действия владельца канала</span><span class="sxs-lookup"><span data-stu-id="4994c-150">Circuit Owner operations</span></span>

<span data-ttu-id="4994c-151">**toocreate авторизации**</span><span class="sxs-lookup"><span data-stu-id="4994c-151">**toocreate an authorization**</span></span>

<span data-ttu-id="4994c-152">Hello владельца канала создает авторизации, который создает ключ авторизации, который может быть используемые tooconnect пользователя канала их toohello шлюзы виртуальной сети канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4994c-152">hello Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="4994c-153">Разрешение действительно только для одного подключения.</span><span class="sxs-lookup"><span data-stu-id="4994c-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="4994c-154">Следующий пример показывает как Hello toocreate авторизации:</span><span class="sxs-lookup"><span data-stu-id="4994c-154">hello following example shows how toocreate an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="4994c-155">Hello ответ содержит ключ авторизации hello и состояние:</span><span class="sxs-lookup"><span data-stu-id="4994c-155">hello response contains hello authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="4994c-156">**tooreview авторизации**</span><span class="sxs-lookup"><span data-stu-id="4994c-156">**tooreview authorizations**</span></span>

<span data-ttu-id="4994c-157">Hello владельцем канала, можно просмотреть все разрешения, выданные для конкретного канала, выполнив следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="4994c-157">hello Circuit Owner can review all authorizations that are issued on a particular circuit by running hello following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="4994c-158">**tooadd авторизации**</span><span class="sxs-lookup"><span data-stu-id="4994c-158">**tooadd authorizations**</span></span>

<span data-ttu-id="4994c-159">Hello владельца канала можно добавить параметры авторизации, используя следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="4994c-159">hello Circuit Owner can add authorizations by using hello following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="4994c-160">**toodelete авторизации**</span><span class="sxs-lookup"><span data-stu-id="4994c-160">**toodelete authorizations**</span></span>

<span data-ttu-id="4994c-161">Hello владелец канала может revoke и удаление авторизации пользователя toohello, выполнив следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="4994c-161">hello Circuit Owner can revoke/delete authorizations toohello user by running hello following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="4994c-162">Действия пользователя канала</span><span class="sxs-lookup"><span data-stu-id="4994c-162">Circuit User operations</span></span>

<span data-ttu-id="4994c-163">Hello пользователя канала требуется идентификатор однорангового hello и ключ авторизации из hello владельца канала.</span><span class="sxs-lookup"><span data-stu-id="4994c-163">hello Circuit User needs hello peer ID and an authorization key from hello Circuit Owner.</span></span> <span data-ttu-id="4994c-164">ключ авторизации Hello представляет собой идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="4994c-164">hello authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="4994c-165">**tooredeem авторизации подключения**</span><span class="sxs-lookup"><span data-stu-id="4994c-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="4994c-166">Hello пользователя канала можно выполнять следующие tooredeem пример hello авторизации:</span><span class="sxs-lookup"><span data-stu-id="4994c-166">hello Circuit User can run hello following example tooredeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="4994c-167">**toorelease авторизации подключения**</span><span class="sxs-lookup"><span data-stu-id="4994c-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="4994c-168">Авторизации можно освободить путем удаления соединений hello, связывающий hello цепь ExpressRoute toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="4994c-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4994c-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4994c-169">Next steps</span></span>

<span data-ttu-id="4994c-170">Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="4994c-170">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
