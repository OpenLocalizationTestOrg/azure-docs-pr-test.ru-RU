---
title: "Устаревшие SKU шлюзов виртуальной сети Azure | Документация Майкрософт"
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
ms.openlocfilehash: 3b2126b1ecd1613950bbf311ae08fafd4af0d51f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="e5142-103">Работа со SKU шлюза виртуальной сети (старые версии SKU)</span><span class="sxs-lookup"><span data-stu-id="e5142-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="e5142-104">Эта статья содержит сведения о старых версиях SKU шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e5142-104">This article contains information about the legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="e5142-105">Старые версий SKU по-прежнему работают в обеих моделях развертывания для созданных VPN-шлюзов.</span><span class="sxs-lookup"><span data-stu-id="e5142-105">The legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="e5142-106">Классические VPN-шлюзы по-прежнему используют старые номера SKU как для имеющихся шлюзов, так и для новых.</span><span class="sxs-lookup"><span data-stu-id="e5142-106">Classic VPN gateways continue to use the legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="e5142-107">При создании VPN-шлюзов диспетчера ресурсов используйте новые номера SKU шлюза.</span><span class="sxs-lookup"><span data-stu-id="e5142-107">When creating new Resource Manager VPN gateways, use the new gateway SKUs.</span></span> <span data-ttu-id="e5142-108">Сведения о новых номерах SKU см. в статье [Основные сведения о VPN-шлюзах Azure](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="e5142-108">For information about the new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="e5142-109"><a name="gwsku"></a>SKU шлюзов</span><span class="sxs-lookup"><span data-stu-id="e5142-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="e5142-110"><a name="agg"></a>Расчетная суммарная пропускная способность в зависимости от SKU</span><span class="sxs-lookup"><span data-stu-id="e5142-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="e5142-111"><a name="config"></a>Поддерживаемые конфигурации в зависимости от SKU и типа VPN</span><span class="sxs-lookup"><span data-stu-id="e5142-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="e5142-112"><a name="resize"></a>Изменение размера SKU шлюза (изменение SKU шлюза)</span><span class="sxs-lookup"><span data-stu-id="e5142-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="e5142-113">Вы можете изменить номер SKU шлюза в пределах одного семейства SKU.</span><span class="sxs-lookup"><span data-stu-id="e5142-113">You can resize a gateway SKU within the same SKU family.</span></span> <span data-ttu-id="e5142-114">Например, при наличии номера SKU " Стандартный" можно изменить размер до SKU HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="e5142-114">For example, if you have a Standard SKU, you can resize to a HighPerformance SKU.</span></span> <span data-ttu-id="e5142-115">Размер VPN-шлюза невозможно изменить путем перехода от старых SKU на новые семейства SKU.</span><span class="sxs-lookup"><span data-stu-id="e5142-115">You can't resize your VPN gateways between the old SKUs and the new SKU families.</span></span> <span data-ttu-id="e5142-116">Например, вы не сможете перейти со SKU " Стандартный" на SKU VpnGw2.</span><span class="sxs-lookup"><span data-stu-id="e5142-116">For example, you can't go from a Standard SKU to a VpnGw2 SKU.</span></span> 

<span data-ttu-id="e5142-117">Чтобы изменить размер номера SKU шлюза для классической модели развертывания, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e5142-117">To resize a gateway SKU for the classic deployment model, use the following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="e5142-118">Чтобы изменить размер номера SKU шлюза для модели развертывания с помощью Resource Manager, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e5142-118">To resize a gateway SKU for the Resource Manager deployment model, use the following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="e5142-119"><a name="migrate"></a>Переход на новые версии SKU шлюзов</span><span class="sxs-lookup"><span data-stu-id="e5142-119"><a name="migrate"></a>Migrate to the new gateway SKUs</span></span>

<span data-ttu-id="e5142-120">При работе с моделью развертывания с помощью Resource Manager можно перейти к новой версии номеров SKU шлюзов.</span><span class="sxs-lookup"><span data-stu-id="e5142-120">If you are working with the Resource Manager deployment model, you can migrate to the new gateway SKUS.</span></span> <span data-ttu-id="e5142-121">При работе с классической моделью развертывания вы не сможете этого сделать. Вместо этого необходимо использовать старые номера SKU.</span><span class="sxs-lookup"><span data-stu-id="e5142-121">If you are working with the classic deployment model, you can't migrate to the new SKUs and must instead continue to use the legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e5142-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5142-122">Next steps</span></span>

<span data-ttu-id="e5142-123">Дополнительные сведения о новых версиях SKU шлюзов см. в разделе [SKU шлюзов](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="e5142-123">For more information about the new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="e5142-124">Дополнительные сведения о параметрах конфигурации VPN-шлюза см. в [этой статье](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="e5142-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>