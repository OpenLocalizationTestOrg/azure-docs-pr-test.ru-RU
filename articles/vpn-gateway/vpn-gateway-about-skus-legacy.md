---
title: "шлюз виртуальной сети Azure aaaLegacy SKU | Документы Microsoft"
description: "Устаревшие SKU шлюзов виртуальной сети."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="de7df-103">Работа со SKU шлюза виртуальной сети (старые версии SKU)</span><span class="sxs-lookup"><span data-stu-id="de7df-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="de7df-104">Эта статья содержит сведения о hello прежних версий (старая) шлюз виртуальной сети SKU.</span><span class="sxs-lookup"><span data-stu-id="de7df-104">This article contains information about hello legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="de7df-105">прежних версий Hello SKU по-прежнему работать в обеих моделях развертывания для VPN-шлюзов, которые уже были созданы.</span><span class="sxs-lookup"><span data-stu-id="de7df-105">hello legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="de7df-106">Классический VPN-шлюзов продолжить toouse hello устаревших SKU, и для существующего шлюзов, так и для новых шлюзов.</span><span class="sxs-lookup"><span data-stu-id="de7df-106">Classic VPN gateways continue toouse hello legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="de7df-107">При создании нового диспетчера ресурсов VPN шлюзы, используйте новый шлюз hello SKU.</span><span class="sxs-lookup"><span data-stu-id="de7df-107">When creating new Resource Manager VPN gateways, use hello new gateway SKUs.</span></span> <span data-ttu-id="de7df-108">Сведения о hello содержатся новых SKU [о VPN-шлюз](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="de7df-108">For information about hello new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="de7df-109"><a name="gwsku"></a>SKU шлюзов</span><span class="sxs-lookup"><span data-stu-id="de7df-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="de7df-110"><a name="agg"></a>Расчетная суммарная пропускная способность в зависимости от SKU</span><span class="sxs-lookup"><span data-stu-id="de7df-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="de7df-111"><a name="config"></a>Поддерживаемые конфигурации в зависимости от SKU и типа VPN</span><span class="sxs-lookup"><span data-stu-id="de7df-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="de7df-112"><a name="resize"></a>Изменение размера SKU шлюза (изменение SKU шлюза)</span><span class="sxs-lookup"><span data-stu-id="de7df-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="de7df-113">Вы можете изменить размер номер SKU шлюза в hello родственного SKU.</span><span class="sxs-lookup"><span data-stu-id="de7df-113">You can resize a gateway SKU within hello same SKU family.</span></span> <span data-ttu-id="de7df-114">Например при наличии стандартном номере SKU, можно изменить размер tooa высокопроизводительные SKU.</span><span class="sxs-lookup"><span data-stu-id="de7df-114">For example, if you have a Standard SKU, you can resize tooa HighPerformance SKU.</span></span> <span data-ttu-id="de7df-115">Не удается изменить размер VPN шлюзы между hello старого SKU и hello новых семейств SKU.</span><span class="sxs-lookup"><span data-stu-id="de7df-115">You can't resize your VPN gateways between hello old SKUs and hello new SKU families.</span></span> <span data-ttu-id="de7df-116">Например не может перейти в стандартном номере SKU tooa VpnGw2 SKU.</span><span class="sxs-lookup"><span data-stu-id="de7df-116">For example, you can't go from a Standard SKU tooa VpnGw2 SKU.</span></span> 

<span data-ttu-id="de7df-117">tooresize номер SKU шлюза для hello классической модели развертывания, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="de7df-117">tooresize a gateway SKU for hello classic deployment model, use hello following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="de7df-118">tooresize номер SKU шлюза для hello модели развертывания диспетчера ресурсов, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="de7df-118">tooresize a gateway SKU for hello Resource Manager deployment model, use hello following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="de7df-119"><a name="migrate"></a>Перенос toohello новый шлюз SKU</span><span class="sxs-lookup"><span data-stu-id="de7df-119"><a name="migrate"></a>Migrate toohello new gateway SKUs</span></span>

<span data-ttu-id="de7df-120">При работе с моделью развертывания диспетчера ресурсов hello можно перенести новый шлюз toohello номера SKU.</span><span class="sxs-lookup"><span data-stu-id="de7df-120">If you are working with hello Resource Manager deployment model, you can migrate toohello new gateway SKUS.</span></span> <span data-ttu-id="de7df-121">При работе с hello классической модели развертывания, которые нельзя перенести toohello новых SKU и вместо этого необходимо продолжить toouse hello SKU прежних версий.</span><span class="sxs-lookup"><span data-stu-id="de7df-121">If you are working with hello classic deployment model, you can't migrate toohello new SKUs and must instead continue toouse hello legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="de7df-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de7df-122">Next steps</span></span>

<span data-ttu-id="de7df-123">Дополнительные сведения о hello новых SKU шлюза см. в разделе [SKU шлюза](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="de7df-123">For more information about hello new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="de7df-124">Дополнительные сведения о параметрах конфигурации VPN-шлюза см. в [этой статье](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="de7df-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>