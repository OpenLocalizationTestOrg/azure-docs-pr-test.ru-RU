---
title: "aaaOverview из BGP со шлюзами VPN Azure | Документы Microsoft"
description: "В статье описывается использование BGP с VPN-шлюзами Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a><span data-ttu-id="1399e-103">Обзор использования BGP с VPN-шлюзами Azure </span><span class="sxs-lookup"><span data-stu-id="1399e-103">Overview of BGP with Azure VPN Gateways</span></span>
<span data-ttu-id="1399e-104">В этой статье описываются особенности использования протокола BGP для VPN-шлюзов Azure.</span><span class="sxs-lookup"><span data-stu-id="1399e-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span></span>

<span data-ttu-id="1399e-105">BGP — hello протокол маршрутизации обычно используется в hello информации через Интернет tooexchange маршрутизации и возможности доступа между двумя или более сетями.</span><span class="sxs-lookup"><span data-stu-id="1399e-105">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="1399e-106">Когда используется в контексте hello виртуальные сети Azure, BGP включает hello Azure VPN-шлюзов и VPN-устройства локальной вызывается узлов BGP или соседей tooexchange» направляет», сообщит обоих шлюзов на hello доступности и возможности доступа для тех, кто префиксы toogo через hello шлюзы или маршрутизаторы участвующих.</span><span class="sxs-lookup"><span data-stu-id="1399e-106">When used in hello context of Azure Virtual Networks, BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="1399e-107">BGP можно также включить транзитной маршрутизацией среди нескольких сетей, распространение маршрутов BGP шлюз узнает из одного tooall однорангового узла BGP других узлов BGP.</span><span class="sxs-lookup"><span data-stu-id="1399e-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span> 

## <a name="why-use-bgp"></a><span data-ttu-id="1399e-108">Почему именно BGP?</span><span class="sxs-lookup"><span data-stu-id="1399e-108">Why use BGP?</span></span>
<span data-ttu-id="1399e-109">BGP не является обязательным протоколом для VPN-шлюзов Azure с использованием маршрутов.</span><span class="sxs-lookup"><span data-stu-id="1399e-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span></span> <span data-ttu-id="1399e-110">Также необходимо убедиться, что VPN-устройства локальной поддерживает BGP, прежде чем включать функцию hello.</span><span class="sxs-lookup"><span data-stu-id="1399e-110">You should also make sure your on-premises VPN devices support BGP before you enable hello feature.</span></span> <span data-ttu-id="1399e-111">Вы можете продолжить toouse VPN-шлюзы Azure и локальным VPN-устройств без BGP.</span><span class="sxs-lookup"><span data-stu-id="1399e-111">You can continue toouse Azure VPN gateways and your on-premises VPN devices without BGP.</span></span> <span data-ttu-id="1399e-112">Здравствуйте, эквивалентные значению с помощью статических маршрутов (без BGP) является *и* с помощью динамической маршрутизации с протоколом BGP между сетями и Azure.</span><span class="sxs-lookup"><span data-stu-id="1399e-112">It is hello equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span></span>

<span data-ttu-id="1399e-113">Преимущества и возможности протокола BGP:</span><span class="sxs-lookup"><span data-stu-id="1399e-113">There are several advantages and new capabilities with BGP:</span></span>

### <a name="support-automatic-and-flexible-prefix-updates"></a><span data-ttu-id="1399e-114">Поддержка автоматического и гибкого обновления префиксов</span><span class="sxs-lookup"><span data-stu-id="1399e-114">Support automatic and flexible prefix updates</span></span>
<span data-ttu-id="1399e-115">С помощью протокола BGP достаточно toodeclare tooa минимальное префикс конкретного узла BGP через туннель IPsec S2S VPN hello.</span><span class="sxs-lookup"><span data-stu-id="1399e-115">With BGP, you only need toodeclare a minimum prefix tooa specific BGP peer over hello IPsec S2S VPN tunnel.</span></span> <span data-ttu-id="1399e-116">Это может быть как префикс узла (/ 32) из hello IP-адрес узла BGP локального VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="1399e-116">It can be as small as a host prefix (/32) of hello BGP peer IP address of your on-premises VPN device.</span></span> <span data-ttu-id="1399e-117">Можно управлять которой локальные префиксы сети, требуется tooadvertise tooAzure tooallow tooaccess вашей виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="1399e-117">You can control which on-premises network prefixes you want tooadvertise tooAzure tooallow your Azure Virtual Network tooaccess.</span></span>

<span data-ttu-id="1399e-118">Также можно объявлять более крупные префиксы, в том числе некоторые префиксы адресов виртуальной сети, например большое пространство частных IP-адресов (10.0.0.0/8 и т. д.).</span><span class="sxs-lookup"><span data-stu-id="1399e-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span></span> <span data-ttu-id="1399e-119">Обратите внимание на то, что префиксы hello не должно совпадать с одним из префиксов вашей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="1399e-119">Note though hello prefixes cannot be identical with any one of your VNet prefixes.</span></span> <span data-ttu-id="1399e-120">Эти префиксы маршруты идентичные tooyour виртуальной сети, будут отклонены.</span><span class="sxs-lookup"><span data-stu-id="1399e-120">Those routes identical tooyour VNet prefixes will be rejected.</span></span>

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a><span data-ttu-id="1399e-121">Поддержка нескольких туннелей между виртуальной сетью и локальным сайтом с автоматической отработкой отказа на основе BGP</span><span class="sxs-lookup"><span data-stu-id="1399e-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span></span>
<span data-ttu-id="1399e-122">Можно установить несколько подключений между вашей виртуальной сети Azure и локальным VPN-устройства в hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="1399e-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in hello same location.</span></span> <span data-ttu-id="1399e-123">Эта возможность предоставляет несколько туннелей (путей) между двумя сетями hello в конфигурации активный активный.</span><span class="sxs-lookup"><span data-stu-id="1399e-123">This capability provides multiple tunnels (paths) between hello two networks in an active-active configuration.</span></span> <span data-ttu-id="1399e-124">Если один из туннелей hello отключен, hello соответствующие маршруты будут сняты через BGP и трафик hello автоматически переходит toohello оставшиеся туннелей.</span><span class="sxs-lookup"><span data-stu-id="1399e-124">If one of hello tunnels is disconnected, hello corresponding routes will be withdrawn via BGP and hello traffic automatically shifts toohello remaining tunnels.</span></span>

<span data-ttu-id="1399e-125">Hello, следующая схема показывает простой пример настройки высокой доступности:</span><span class="sxs-lookup"><span data-stu-id="1399e-125">hello following diagram shows a simple example of this highly available setup:</span></span>

![Несколько активных путей](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a><span data-ttu-id="1399e-127">Поддержка транзитной маршрутизации между локальными сетями и несколькими виртуальными сетями Azure</span><span class="sxs-lookup"><span data-stu-id="1399e-127">Support transit routing between your on-premises networks and multiple Azure VNets</span></span>
<span data-ttu-id="1399e-128">BGP включает несколько шлюзов toolearn и распространить префиксы из разных сетях ли они прямо или косвенно подключены.</span><span class="sxs-lookup"><span data-stu-id="1399e-128">BGP enables multiple gateways toolearn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span></span> <span data-ttu-id="1399e-129">Благодаря этому возможна транзитная маршрутизация через VPN-шлюзы Azure между локальными сайтами или несколькими виртуальными сетями Azure.</span><span class="sxs-lookup"><span data-stu-id="1399e-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span></span>

<span data-ttu-id="1399e-130">Hello следующей диаграмме показан пример мульти-прыжка топологии с несколькими путями, которые могут проходить трафика между hello двумя локальными сетями через VPN-шлюзы Azure в сетях Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="1399e-130">hello following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between hello two on-premises networks through Azure VPN gateways within hello Microsoft Networks:</span></span>

![Многоскачковый транзит](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a><span data-ttu-id="1399e-132">Часто задаваемые вопросы о BGP</span><span class="sxs-lookup"><span data-stu-id="1399e-132">BGP FAQ</span></span>
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1399e-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1399e-133">Next steps</span></span>
<span data-ttu-id="1399e-134">В разделе [Приступая к работе с протоколом BGP на шлюзах Azure VPN](vpn-gateway-bgp-resource-manager-ps.md) для действия tooconfigure BGP для подключения к виртуальной сети для виртуальной сети и между организациями.</span><span class="sxs-lookup"><span data-stu-id="1399e-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps tooconfigure BGP for your cross-premises and VNet-to-VNet connections.</span></span>

