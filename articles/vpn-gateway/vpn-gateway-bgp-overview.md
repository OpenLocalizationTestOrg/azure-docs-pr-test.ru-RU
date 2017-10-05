---
title: "Особенности использования BGP с VPN-шлюзами Azure | Документация Майкрософт"
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
ms.openlocfilehash: 60d8dd45ecbd4a075721c25acadb21d4e2fd5448
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a><span data-ttu-id="92c5d-103">Обзор использования BGP с VPN-шлюзами Azure </span><span class="sxs-lookup"><span data-stu-id="92c5d-103">Overview of BGP with Azure VPN Gateways</span></span>
<span data-ttu-id="92c5d-104">В этой статье описываются особенности использования протокола BGP для VPN-шлюзов Azure.</span><span class="sxs-lookup"><span data-stu-id="92c5d-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span></span>

<span data-ttu-id="92c5d-105">Стандартный протокол маршрутизации BGP обычно используется в Интернете для обмена данными о маршрутизации и доступности между двумя или несколькими сетями.</span><span class="sxs-lookup"><span data-stu-id="92c5d-105">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="92c5d-106">В контексте виртуальных сетей Azure протокол BGP используется VPN-шлюзами Azure и локальными VPN-устройствами (так называемые узлы BGP) для обмена данными о маршрутах. Это позволяет информировать участников обмена о доступности и возможности передавать префиксы через шлюзы или маршрутизаторы.</span><span class="sxs-lookup"><span data-stu-id="92c5d-106">When used in the context of Azure Virtual Networks, BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="92c5d-107">Также BGP позволяет передавать трафик транзитом через несколько сетей. Для этого шлюз BGP распространяет на все известные ему узлы BGP информацию о маршрутах, полученную от остальных узлов BGP.</span><span class="sxs-lookup"><span data-stu-id="92c5d-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span> 

## <a name="why-use-bgp"></a><span data-ttu-id="92c5d-108">Почему именно BGP?</span><span class="sxs-lookup"><span data-stu-id="92c5d-108">Why use BGP?</span></span>
<span data-ttu-id="92c5d-109">BGP не является обязательным протоколом для VPN-шлюзов Azure с использованием маршрутов.</span><span class="sxs-lookup"><span data-stu-id="92c5d-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span></span> <span data-ttu-id="92c5d-110">Также до включения протокола BGP следует убедиться, что ваши локальные VPN-устройства поддерживают его.</span><span class="sxs-lookup"><span data-stu-id="92c5d-110">You should also make sure your on-premises VPN devices support BGP before you enable the feature.</span></span> <span data-ttu-id="92c5d-111">Вы можете продолжать использовать VPN-шлюзы Azure и локальные VPN-устройства без протокола BGP.</span><span class="sxs-lookup"><span data-stu-id="92c5d-111">You can continue to use Azure VPN gateways and your on-premises VPN devices without BGP.</span></span> <span data-ttu-id="92c5d-112">Для обмена данными между сетями и Azure можно использовать статические маршруты (без BGP) *или* динамическую маршрутизацию по протоколу BGP.</span><span class="sxs-lookup"><span data-stu-id="92c5d-112">It is the equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span></span>

<span data-ttu-id="92c5d-113">Преимущества и возможности протокола BGP:</span><span class="sxs-lookup"><span data-stu-id="92c5d-113">There are several advantages and new capabilities with BGP:</span></span>

### <a name="support-automatic-and-flexible-prefix-updates"></a><span data-ttu-id="92c5d-114">Поддержка автоматического и гибкого обновления префиксов</span><span class="sxs-lookup"><span data-stu-id="92c5d-114">Support automatic and flexible prefix updates</span></span>
<span data-ttu-id="92c5d-115">Если используется протокол BGP, достаточно объявить минимальный префикс для определенного узла BGP через VPN-туннель IPsec S2S.</span><span class="sxs-lookup"><span data-stu-id="92c5d-115">With BGP, you only need to declare a minimum prefix to a specific BGP peer over the IPsec S2S VPN tunnel.</span></span> <span data-ttu-id="92c5d-116">Это может быть даже небольшой префикс узла (/32) для IP-адреса узла BGP на локальном VPN-устройстве.</span><span class="sxs-lookup"><span data-stu-id="92c5d-116">It can be as small as a host prefix (/32) of the BGP peer IP address of your on-premises VPN device.</span></span> <span data-ttu-id="92c5d-117">Вы можете выбирать, какие из локальных префиксов будут объявлены в Azure, чтобы виртуальная сеть Azure получила к ним доступ.</span><span class="sxs-lookup"><span data-stu-id="92c5d-117">You can control which on-premises network prefixes you want to advertise to Azure to allow your Azure Virtual Network to access.</span></span>

<span data-ttu-id="92c5d-118">Также можно объявлять более крупные префиксы, в том числе некоторые префиксы адресов виртуальной сети, например большое пространство частных IP-адресов (10.0.0.0/8 и т. д.).</span><span class="sxs-lookup"><span data-stu-id="92c5d-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span></span> <span data-ttu-id="92c5d-119">Обратите внимание, что эти префиксы не должны совпадать с префиксами виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="92c5d-119">Note though the prefixes cannot be identical with any one of your VNet prefixes.</span></span> <span data-ttu-id="92c5d-120">Маршруты, идентичные префиксам виртуальной сети, будут отклонены.</span><span class="sxs-lookup"><span data-stu-id="92c5d-120">Those routes identical to your VNet prefixes will be rejected.</span></span>

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a><span data-ttu-id="92c5d-121">Поддержка нескольких туннелей между виртуальной сетью и локальным сайтом с автоматической отработкой отказа на основе BGP</span><span class="sxs-lookup"><span data-stu-id="92c5d-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span></span>
<span data-ttu-id="92c5d-122">Вы можете создавать несколько подключений между виртуальной сетью Azure и локальными VPN-устройствами в одном расположении.</span><span class="sxs-lookup"><span data-stu-id="92c5d-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in the same location.</span></span> <span data-ttu-id="92c5d-123">Это позволяет использовать между двумя сетями несколько туннелей (путей) в режиме "активный — активный".</span><span class="sxs-lookup"><span data-stu-id="92c5d-123">This capability provides multiple tunnels (paths) between the two networks in an active-active configuration.</span></span> <span data-ttu-id="92c5d-124">Если один из туннелей отключится, BGP отзовет соответствующие маршруты и трафик автоматически переместится в действующие туннели.</span><span class="sxs-lookup"><span data-stu-id="92c5d-124">If one of the tunnels is disconnected, the corresponding routes will be withdrawn via BGP and the traffic automatically shifts to the remaining tunnels.</span></span>

<span data-ttu-id="92c5d-125">Следующая схема содержит простой пример настройки с высокой доступностью.</span><span class="sxs-lookup"><span data-stu-id="92c5d-125">The following diagram shows a simple example of this highly available setup:</span></span>

![Несколько активных путей](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a><span data-ttu-id="92c5d-127">Поддержка транзитной маршрутизации между локальными сетями и несколькими виртуальными сетями Azure</span><span class="sxs-lookup"><span data-stu-id="92c5d-127">Support transit routing between your on-premises networks and multiple Azure VNets</span></span>
<span data-ttu-id="92c5d-128">BGP позволяет нескольким шлюзам получать и распространять префиксы из разных сетей, подключенных к ним напрямую или опосредованно.</span><span class="sxs-lookup"><span data-stu-id="92c5d-128">BGP enables multiple gateways to learn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span></span> <span data-ttu-id="92c5d-129">Благодаря этому возможна транзитная маршрутизация через VPN-шлюзы Azure между локальными сайтами или несколькими виртуальными сетями Azure.</span><span class="sxs-lookup"><span data-stu-id="92c5d-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span></span>

<span data-ttu-id="92c5d-130">Следующая схема содержит пример многоскачковой топологии с несколькими путями, по которым трафик может проходить между двумя локальными сетями через VPN-шлюзы Azure в сети Microsoft.</span><span class="sxs-lookup"><span data-stu-id="92c5d-130">The following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between the two on-premises networks through Azure VPN gateways within the Microsoft Networks:</span></span>

![Многоскачковый транзит](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a><span data-ttu-id="92c5d-132">Часто задаваемые вопросы о BGP</span><span class="sxs-lookup"><span data-stu-id="92c5d-132">BGP FAQ</span></span>
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="92c5d-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="92c5d-133">Next steps</span></span>
<span data-ttu-id="92c5d-134">Действия по настройке BGP для межсистемных подключений и подключений между виртуальными сетями описаны в разделе [Настройка BGP на VPN-шлюзах Azure с помощью Azure Resource Manager и PowerShell](vpn-gateway-bgp-resource-manager-ps.md) .</span><span class="sxs-lookup"><span data-stu-id="92c5d-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps to configure BGP for your cross-premises and VNet-to-VNet connections.</span></span>

