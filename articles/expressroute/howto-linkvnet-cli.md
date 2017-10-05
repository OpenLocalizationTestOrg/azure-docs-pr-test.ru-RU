---
title: "Подключение виртуальной сети к каналу ExpressRoute с помощью Azure CLI | Документация Майкрософт"
description: "В этом документе содержатся общие сведения о связывании виртуальных сетей с каналами ExpressRoute с помощью модели развертывания Resource Manager и интерфейса командной строки (CLI)."
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
ms.openlocfilehash: 0ea696e796ec3a943bc028f56da417978b728b82
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-cli"></a><span data-ttu-id="886fe-103">Подключение виртуальной сети к каналу ExpressRoute с помощью CLI</span><span class="sxs-lookup"><span data-stu-id="886fe-103">Connect a virtual network to an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="886fe-104">Эта статья поможет вам связать виртуальные сети с каналами Azure ExpressRoute с помощью CLI.</span><span class="sxs-lookup"><span data-stu-id="886fe-104">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="886fe-105">С помощью Azure CLI можно связывать только виртуальные сети, созданные по модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="886fe-105">To link using Azure CLI, the virtual networks must be created using the Resource Manager deployment model.</span></span> <span data-ttu-id="886fe-106">Они могут входить в одну и ту же подписку или в разные подписки.</span><span class="sxs-lookup"><span data-stu-id="886fe-106">They can either be in the same subscription, or part of another subscription.</span></span> <span data-ttu-id="886fe-107">Для подключения виртуальной сети к каналу ExpressRoute можно использовать другие методы, информация о которых приводится в статьях из следующего списка:</span><span class="sxs-lookup"><span data-stu-id="886fe-107">If you want to use a different method to connect your VNet to an ExpressRoute circuit, you can select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="886fe-108">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="886fe-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="886fe-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="886fe-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="886fe-110">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="886fe-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="886fe-111">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="886fe-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="886fe-112">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="886fe-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="886fe-113">Предварительные требования для настройки</span><span class="sxs-lookup"><span data-stu-id="886fe-113">Configuration prerequisites</span></span>

* <span data-ttu-id="886fe-114">Требуется последняя версия интерфейса командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="886fe-114">You need the latest version of the command-line interface (CLI).</span></span> <span data-ttu-id="886fe-115">Дополнительные сведения см. в статье [Установка Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="886fe-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="886fe-116">Прежде чем приступить к настройке, необходимо изучить [предварительные требования](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md) и [рабочие процессы](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="886fe-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="886fe-117">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="886fe-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="886fe-118">Следуйте инструкциям, чтобы [создать канал ExpressRoute](howto-circuit-cli.md) и включить его на стороне поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="886fe-118">Follow the instructions to [create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="886fe-119">Убедитесь, что для вашего канала настроен частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="886fe-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="886fe-120">Инструкции по маршрутизации см. в статье [Настройка маршрутизации](howto-routing-cli.md).</span><span class="sxs-lookup"><span data-stu-id="886fe-120">See the [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="886fe-121">Убедитесь, что настроен частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="886fe-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="886fe-122">Для создания сквозного подключения потребуется также пиринг BGP между вашей сетью и сетью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="886fe-122">The BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="886fe-123">Вам необходимо создать и полностью подготовить виртуальную сеть и шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="886fe-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="886fe-124">Следуйте инструкциям по [созданию шлюза виртуальной сети для ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="886fe-124">Follow the instructions to [Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="886fe-125">Обязательно используйте `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="886fe-125">Be sure to use `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="886fe-126">К стандартному каналу ExpressRoute можно подключить не более 10 виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="886fe-126">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="886fe-127">Если используется стандартный канал ExpressRoute, все виртуальные сети должны находиться в одном геополитическом регионе.</span><span class="sxs-lookup"><span data-stu-id="886fe-127">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="886fe-128">Если вы включите надстройку ExpressRoute Premium, вы сможете подключить к каналу ExpressRoute больше виртуальных сетей или подключить сеть из другого геополитического региона.</span><span class="sxs-lookup"><span data-stu-id="886fe-128">If you enable the ExpressRoute premium add-on, you can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="886fe-129">Дополнительные сведения о надстройке версии Premium см. в статье [Вопросы и ответы по ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="886fe-129">For more information about the premium add-on, see the [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="886fe-130">Подключение к каналу виртуальной сети в той же подписке</span><span class="sxs-lookup"><span data-stu-id="886fe-130">Connect a virtual network in the same subscription to a circuit</span></span>

<span data-ttu-id="886fe-131">Вы можете связать шлюз виртуальной сети с каналом ExpressRoute, используя приведенный ниже пример.</span><span class="sxs-lookup"><span data-stu-id="886fe-131">You can connect a virtual network gateway to an ExpressRoute circuit by using the example.</span></span> <span data-ttu-id="886fe-132">Прежде чем выполнять эту команду, убедитесь, что шлюз виртуальной сети существует и готов к связыванию.</span><span class="sxs-lookup"><span data-stu-id="886fe-132">Make sure that the virtual network gateway is created and is ready for linking before you run the command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="886fe-133">Подключение к каналу виртуальной сети в другой подписке</span><span class="sxs-lookup"><span data-stu-id="886fe-133">Connect a virtual network in a different subscription to a circuit</span></span>

<span data-ttu-id="886fe-134">Канал ExpressRoute может совместно использоваться несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="886fe-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="886fe-135">На рисунке ниже схематично показан способ совместного использования каналов ExpressRoute несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="886fe-135">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="886fe-136">Каждое маленькое облако внутри большого облака представляет подписки, принадлежащие различным подразделениям одной организации.</span><span class="sxs-lookup"><span data-stu-id="886fe-136">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="886fe-137">Любое подразделение в организации может использовать свою собственную подписку для развертывания служб. Кроме того, оно может совместно использовать один выделенный канал ExpressRoute для подключения к корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="886fe-137">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="886fe-138">Владельцем канала ExpressRoute может выступать одно подразделение (в данном примере — ИТ-подразделение).</span><span class="sxs-lookup"><span data-stu-id="886fe-138">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="886fe-139">Другие подписки в организации могут использовать канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="886fe-139">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="886fe-140">Плата за подключение и использование пропускной способности выделенного канала взимается с владельца канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="886fe-140">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="886fe-141">Полоса пропускания распределяется между всеми виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="886fe-141">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Подключение между подписками](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="886fe-143">Администрирование: владельцы и пользователи канала</span><span class="sxs-lookup"><span data-stu-id="886fe-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="886fe-144">Владельцем канала считается уполномоченный опытный пользователь ресурса канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="886fe-144">The 'Circuit Owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="886fe-145">Владелец канала может создавать разрешения, которые будут использовать пользователи канала.</span><span class="sxs-lookup"><span data-stu-id="886fe-145">The Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="886fe-146">Пользователями канала считаются владельцы шлюзов виртуальных сетей, не включенных в подписку, к которой относится канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="886fe-146">Circuit Users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="886fe-147">Пользователи канала могут использовать разрешения (по одному разрешению на виртуальную сеть).</span><span class="sxs-lookup"><span data-stu-id="886fe-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="886fe-148">Владелец канала имеет право в любой момент изменить или отменить эти разрешения.</span><span class="sxs-lookup"><span data-stu-id="886fe-148">The Circuit Owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="886fe-149">Отмена разрешения приводит к удалению всех связывающих подключений из подписки, для которой был отменен доступ.</span><span class="sxs-lookup"><span data-stu-id="886fe-149">When an authorization is revoked, all link connections are deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="886fe-150">Действия владельца канала</span><span class="sxs-lookup"><span data-stu-id="886fe-150">Circuit Owner operations</span></span>

<span data-ttu-id="886fe-151">**Создание разрешения**</span><span class="sxs-lookup"><span data-stu-id="886fe-151">**To create an authorization**</span></span>

<span data-ttu-id="886fe-152">Владелец канала создает разрешение, в результате чего создается ключ, с помощью которого пользователь канала сможет подключить шлюзы виртуальной сети к каналу ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="886fe-152">The Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="886fe-153">Разрешение действительно только для одного подключения.</span><span class="sxs-lookup"><span data-stu-id="886fe-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="886fe-154">В следующем примере показано, как создать разрешение.</span><span class="sxs-lookup"><span data-stu-id="886fe-154">The following example shows how to create an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="886fe-155">Ответ содержит ключ и состояние разрешения.</span><span class="sxs-lookup"><span data-stu-id="886fe-155">The response contains the authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="886fe-156">**Просмотр разрешений**</span><span class="sxs-lookup"><span data-stu-id="886fe-156">**To review authorizations**</span></span>

<span data-ttu-id="886fe-157">Владелец канала может просмотреть все разрешения, выданные для определенного канала, выполнив команду из следующего примера.</span><span class="sxs-lookup"><span data-stu-id="886fe-157">The Circuit Owner can review all authorizations that are issued on a particular circuit by running the following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="886fe-158">**Добавление разрешений**</span><span class="sxs-lookup"><span data-stu-id="886fe-158">**To add authorizations**</span></span>

<span data-ttu-id="886fe-159">Владелец канала может добавлять разрешения с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="886fe-159">The Circuit Owner can add authorizations by using the following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="886fe-160">**Удаление разрешений**</span><span class="sxs-lookup"><span data-stu-id="886fe-160">**To delete authorizations**</span></span>

<span data-ttu-id="886fe-161">Владелец канала может отменять и удалять разрешения, выданные пользователю, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="886fe-161">The Circuit Owner can revoke/delete authorizations to the user by running the following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="886fe-162">Действия пользователя канала</span><span class="sxs-lookup"><span data-stu-id="886fe-162">Circuit User operations</span></span>

<span data-ttu-id="886fe-163">Пользователь канала должен получить идентификатор однорангового узла и ключ разрешения от владельца канала.</span><span class="sxs-lookup"><span data-stu-id="886fe-163">The Circuit User needs the peer ID and an authorization key from the Circuit Owner.</span></span> <span data-ttu-id="886fe-164">Ключ разрешения представляет собой идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="886fe-164">The authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="886fe-165">**Активация разрешения на подключение**</span><span class="sxs-lookup"><span data-stu-id="886fe-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="886fe-166">Пользователь канала может активировать разрешение на подключение, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="886fe-166">The Circuit User can run the following example to redeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="886fe-167">**Освобождение разрешения на подключение**</span><span class="sxs-lookup"><span data-stu-id="886fe-167">**To release a connection authorization**</span></span>

<span data-ttu-id="886fe-168">Разрешение можно освободить, удалив подключение, связывающее канал ExpressRoute и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="886fe-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="886fe-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="886fe-169">Next steps</span></span>

<span data-ttu-id="886fe-170">Дополнительные сведения об ExpressRoute см. в статье [Вопросы и ответы по ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="886fe-170">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>