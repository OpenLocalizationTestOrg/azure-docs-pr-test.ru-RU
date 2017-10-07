---
title: "Наблюдатель сети Azure прыжке toonext aaaIntroduction | Документы Microsoft"
description: "Эта страница Обзор hello Наблюдатель сети возможность следующего прыжка"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a><span data-ttu-id="0a086-103">Введение toonext участке Наблюдатель сети Azure</span><span class="sxs-lookup"><span data-stu-id="0a086-103">Introduction toonext hop in Azure Network Watcher</span></span>

<span data-ttu-id="0a086-104">Трафик от виртуальной Машины, отправляется tooa назначения, в зависимости от действующих маршрутах hello, связанный с адаптером.</span><span class="sxs-lookup"><span data-stu-id="0a086-104">Traffic from a VM is sent tooa destination based on hello effective routes associated with a NIC.</span></span> <span data-ttu-id="0a086-105">Следующий прыжок возвращает тип следующего прыжка hello и IP-адрес пакета из конкретной виртуальной машины и сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="0a086-105">Next hop gets hello next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="0a086-106">Это помогает toodetermine Если hello пакетов, назначения направленной toohello или является поставщик только трафик hello, черный.</span><span class="sxs-lookup"><span data-stu-id="0a086-106">This helps toodetermine if hello packet is being directed toohello destination or is hello traffic being black holed.</span></span> <span data-ttu-id="0a086-107">Неправильной конфигурации маршрутов пользователем hello, где трафика — расширенный tooan локально или виртуального устройства, можно привести tooconnectivity проблемы.</span><span class="sxs-lookup"><span data-stu-id="0a086-107">An improper configuration of routes by hello user, where a traffic is directed tooan on-premises location or a virtual appliance, can lead tooconnectivity issues.</span></span> <span data-ttu-id="0a086-108">Следующий прыжок также возвращает hello таблицы маршрутов, связанной с hello следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="0a086-108">Next hop also returns hello route table associated with hello next hop.</span></span> <span data-ttu-id="0a086-109">При запросе следующего прыжка, если маршрут hello определяется как маршрут определяемых пользователем, будет возвращаться этого маршрута.</span><span class="sxs-lookup"><span data-stu-id="0a086-109">When querying a next hop if hello route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="0a086-110">В противном случае возвращается системный маршрут.</span><span class="sxs-lookup"><span data-stu-id="0a086-110">Otherwise Next hop returns "System Route".</span></span>

![Обзор функции определения следующего прыжка][1]

<span data-ttu-id="0a086-112">Hello ниже приведен список hello следующего прыжка типов, которые могут быть возвращены при выполнении запроса следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="0a086-112">hello following is a list of hello next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="0a086-113">Интернет</span><span class="sxs-lookup"><span data-stu-id="0a086-113">Internet</span></span>
* <span data-ttu-id="0a086-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="0a086-114">VirtualAppliance</span></span>
* <span data-ttu-id="0a086-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="0a086-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="0a086-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="0a086-116">VnetLocal</span></span>
* <span data-ttu-id="0a086-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="0a086-117">HyperNetGateway</span></span>
* <span data-ttu-id="0a086-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="0a086-118">VnetPeering</span></span>
* <span data-ttu-id="0a086-119">None</span><span class="sxs-lookup"><span data-stu-id="0a086-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="0a086-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a086-120">Next steps</span></span>

<span data-ttu-id="0a086-121">Узнайте, как toouse следующего прыжка toofind проблемы с сетевым подключением, посетив [следующего прыжка проверка hello на виртуальной Машине](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0a086-121">Learn how toouse next hop toofind issues with network connectivity by visiting [Check hello next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













