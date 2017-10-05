---
title: "Сведения о шлюзах виртуальных сетей ExpressRoute | Документация Майкрософт"
description: "Сведения о шлюзах виртуальных сетей ExpressRoute."
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: a6363fa380d0bab05d7500141cc6019d1d3f68b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="ca2ba-103">Сведения о шлюзах виртуальных сетей ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ca2ba-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="ca2ba-104">Шлюз виртуальной сети используется для обмена сетевым трафиком между виртуальными и локальными сетями Azure.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="ca2ba-105">В процессе настройки подключения ExpressRoute необходимо создать и настроить шлюз виртуальной сети и подключение для него.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="ca2ba-106">При создании шлюза виртуальной сети нужно указать несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="ca2ba-107">Один из обязательных параметров указывает, будет ли шлюз использоваться для трафика ExpressRoute или VPN "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="ca2ba-107">One of the required settings specifies whether the gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="ca2ba-108">В модели развертывания Resource Manager это параметр -GatewayType.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-108">In the Resource Manager deployment model, the setting is '-GatewayType'.</span></span>

<span data-ttu-id="ca2ba-109">Если сетевой трафик направляется через частное подключение, используется тип шлюза ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-109">When network traffic is sent on a private connection, you use the gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="ca2ba-110">Он также называется шлюзом ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-110">This is also referred to as an ExpressRoute gateway.</span></span> <span data-ttu-id="ca2ba-111">Если сетевой трафик направляется в зашифрованном виде через общедоступный Интернет, то используется тип шлюза Vpn.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-111">When network traffic is sent encrypted across the public Internet, you use the gateway type 'Vpn'.</span></span> <span data-ttu-id="ca2ba-112">Он также называется VPN-шлюзом.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-112">This is referred to as a VPN gateway.</span></span> <span data-ttu-id="ca2ba-113">При подключениях типа "сеть — сеть", "точка — сеть" и "виртуальная сеть — виртуальная сеть" используется VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="ca2ba-114">В виртуальной сети каждому типу шлюза может соответствовать только один шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="ca2ba-115">Например, у вас может быть только один шлюз виртуальной сети типа VPN и только один типа ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="ca2ba-116">Эта статья посвящена шлюзам виртуальных сетей ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-116">This article focuses on the ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="ca2ba-117"><a name="gwsku"></a>SKU шлюзов</span><span class="sxs-lookup"><span data-stu-id="ca2ba-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="ca2ba-118">Если требуется выполнить обновление до шлюза с большими возможностями согласно SKU, в большинстве случаев можно использовать командлет PowerShell Resize-AzureRmVirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-118">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="ca2ba-119">Это подойдет для обновлений до SKU Standard и HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-119">This will work for upgrades to Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="ca2ba-120">Однако для обновления до SKU UltraPerformance шлюз необходимо создать заново.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-120">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span></span>

### <span data-ttu-id="ca2ba-121"><a name="aggthroughput"></a>Расчетная суммарная пропускная способность в зависимости от SKU шлюза</span><span class="sxs-lookup"><span data-stu-id="ca2ba-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="ca2ba-122">В следующей таблице приведены типы шлюзов с приблизительной суммарной пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-122">The following table shows the gateway types and the estimated aggregate throughput.</span></span> <span data-ttu-id="ca2ba-123">Эта таблица относится к классической модели развертывания и модели диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-123">This table applies to both the Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="ca2ba-124">Пропускная способность приложения зависит от нескольких факторов, таких как сквозная задержка и количество потоков трафика, которые открывает приложение.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-124">Application throughput depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span></span> <span data-ttu-id="ca2ba-125">Числа в таблице представляют собой верхний предел, которого приложение может теоретически достичь в идеальных условиях.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-125">The numbers in the table represent the upper limit that the application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="ca2ba-126"><a name="resources"></a>Интерфейсы REST API и командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca2ba-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="ca2ba-127">Дополнительные технические материалы и специальные требования к синтаксису, действующие при использовании интерфейсов REST API и командлетов PowerShell для настройки конфигураций шлюзов виртуальных сетей, доступны по приведенным ниже ссылкам.</span><span class="sxs-lookup"><span data-stu-id="ca2ba-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="ca2ba-128">**Классический**</span><span class="sxs-lookup"><span data-stu-id="ca2ba-128">**Classic**</span></span> | <span data-ttu-id="ca2ba-129">**Диспетчер ресурсов**</span><span class="sxs-lookup"><span data-stu-id="ca2ba-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="ca2ba-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca2ba-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="ca2ba-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca2ba-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="ca2ba-132">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="ca2ba-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="ca2ba-133">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="ca2ba-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="ca2ba-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca2ba-134">Next steps</span></span>
<span data-ttu-id="ca2ba-135">Дополнительные сведения о доступных конфигурациях подключений см. в статье [Технический обзор ExpressRoute](expressroute-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca2ba-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

