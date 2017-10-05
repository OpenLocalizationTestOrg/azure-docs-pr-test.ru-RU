---
title: "Общие сведения о функции определения следующего прыжка в Наблюдателе за сетями Azure | Документация Майкрософт"
description: "Эта страница содержит общие сведения о функции определения следующего прыжка в Наблюдателе за сетями."
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
ms.openlocfilehash: 5dd65d2418cae206965a13013dd990b916ad0733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-next-hop-in-azure-network-watcher"></a><span data-ttu-id="5f0a8-103">Общие сведения о функции определения следующего прыжка в Наблюдателе за сетями Azure</span><span class="sxs-lookup"><span data-stu-id="5f0a8-103">Introduction to next hop in Azure Network Watcher</span></span>

<span data-ttu-id="5f0a8-104">Трафик из виртуальной машины отправляется по назначению в зависимости от действующих маршрутов, связанных с сетевой картой.</span><span class="sxs-lookup"><span data-stu-id="5f0a8-104">Traffic from a VM is sent to a destination based on the effective routes associated with a NIC.</span></span> <span data-ttu-id="5f0a8-105">Функция определения следующего прыжка возвращает тип следующего прыжка и IP-адрес пакета из определенной виртуальной машины и сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="5f0a8-105">Next hop gets the next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="5f0a8-106">Это позволяет определить, направляется ли пакет по назначению или трафик передается в "черную дыру".</span><span class="sxs-lookup"><span data-stu-id="5f0a8-106">This helps to determine if the packet is being directed to the destination or is the traffic being black holed.</span></span> <span data-ttu-id="5f0a8-107">Неправильная настройка маршрутов пользователем, при которой трафик направляется в локальное расположение или на виртуальное устройство, может привести к проблемам подключения.</span><span class="sxs-lookup"><span data-stu-id="5f0a8-107">An improper configuration of routes by the user, where a traffic is directed to an on-premises location or a virtual appliance, can lead to connectivity issues.</span></span> <span data-ttu-id="5f0a8-108">Функция определения следующего прыжка также возвращает таблицу маршрутов, связанную со следующим прыжком.</span><span class="sxs-lookup"><span data-stu-id="5f0a8-108">Next hop also returns the route table associated with the next hop.</span></span> <span data-ttu-id="5f0a8-109">Если при запросе следующего прыжка маршрут задан как определяемый пользователем, то возвращается этот маршрут.</span><span class="sxs-lookup"><span data-stu-id="5f0a8-109">When querying a next hop if the route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="5f0a8-110">В противном случае возвращается системный маршрут.</span><span class="sxs-lookup"><span data-stu-id="5f0a8-110">Otherwise Next hop returns "System Route".</span></span>

![Обзор функции определения следующего прыжка][1]

<span data-ttu-id="5f0a8-112">Ниже приведен список типов следующего прыжка, которые могут быть возвращены при запросе следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="5f0a8-112">The following is a list of the next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="5f0a8-113">Интернет</span><span class="sxs-lookup"><span data-stu-id="5f0a8-113">Internet</span></span>
* <span data-ttu-id="5f0a8-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="5f0a8-114">VirtualAppliance</span></span>
* <span data-ttu-id="5f0a8-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="5f0a8-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="5f0a8-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="5f0a8-116">VnetLocal</span></span>
* <span data-ttu-id="5f0a8-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="5f0a8-117">HyperNetGateway</span></span>
* <span data-ttu-id="5f0a8-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="5f0a8-118">VnetPeering</span></span>
* <span data-ttu-id="5f0a8-119">None</span><span class="sxs-lookup"><span data-stu-id="5f0a8-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="5f0a8-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f0a8-120">Next steps</span></span>

<span data-ttu-id="5f0a8-121">Узнайте, как использовать функцию определения следующего прыжка для поиска проблем с сетевыми подключениями, ознакомившись с разделом [Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal](network-watcher-check-next-hop-portal.md) (Определение типа следующего прыжка с помощью функции определения следующего прыжка в Наблюдателе за сетями на портале).</span><span class="sxs-lookup"><span data-stu-id="5f0a8-121">Learn how to use next hop to find issues with network connectivity by visiting [Check the next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













