---
title: "Общие сведения о проверке IP-потока в Наблюдателе за сетями Azure | Документация Майкрософт"
description: "Эта страница содержит обзор функции проверки IP-потока в Наблюдателе за сетями."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9c0dfc449b3d93d8aa4551ce16476c8313d731fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-ip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="bad83-103">Общие сведения о проверке IP-потока в Наблюдателе за сетями Azure</span><span class="sxs-lookup"><span data-stu-id="bad83-103">Introduction to IP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="bad83-104">Функция проверки IP-потока проверяет, разрешена или запрещена передача пакета на виртуальную машину или с нее на основе данных пяти кортежей.</span><span class="sxs-lookup"><span data-stu-id="bad83-104">IP flow verify checks if a packet is allowed or denied to or from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="bad83-105">Эта информация включает в себя направление, протокол, локальный IP-адрес, удаленный IP-адрес, локальный порт и удаленный порт.</span><span class="sxs-lookup"><span data-stu-id="bad83-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="bad83-106">Если пакет отклонен группой безопасности, возвращается имя правила, которое запретило этот пакет.</span><span class="sxs-lookup"><span data-stu-id="bad83-106">If the packet is denied by a security group, the name of the rule that denied the packet is returned.</span></span> <span data-ttu-id="bad83-107">Хотя может быть выбран любой исходный или конечный IP-адрес, эта функция помогает администраторам быстро диагностировать проблемы с входящим или исходящим подключением к Интернету и входящим или исходящим подключением к локальной среде.</span><span class="sxs-lookup"><span data-stu-id="bad83-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or to the internet and from or to the on-premises environment.</span></span>

<span data-ttu-id="bad83-108">Функция проверки IP-потока нацеливается на сетевой интерфейс виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bad83-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="bad83-109">После чего на основе настроенных параметров проверяется входящий или исходящий поток трафика этого сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="bad83-109">Traffic flow is then verified based on the configured settings to or from that network interface.</span></span> <span data-ttu-id="bad83-110">Эту возможность удобно использовать, чтобы проверить, блокирует ли правило в группе безопасности сети входящий или исходящий трафик виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bad83-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic to or from a virtual machine.</span></span>

<span data-ttu-id="bad83-111">Во всех регионах, в которых планируется выполнять проверку IP-потока, нужно создать экземпляр Наблюдателя за сетями.</span><span class="sxs-lookup"><span data-stu-id="bad83-111">An instance of Network Watcher needs to be created in all regions that you plan to run IP flow verify.</span></span> <span data-ttu-id="bad83-112">Наблюдатель за сетями — это региональная служба, которая может выполняться только для ресурсов в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="bad83-112">Network Watcher is a regional service and can only be ran against resources in the same region.</span></span> <span data-ttu-id="bad83-113">Это не отражается на результатах проверки IP-потока, так как маршрут, связанный с сетевой картой, все равно будет возвращаться.</span><span class="sxs-lookup"><span data-stu-id="bad83-113">This does not affect the results of IP flow verify as the route associated with the NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="bad83-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bad83-115">Next steps</span></span>

<span data-ttu-id="bad83-116">Ознакомьтесь с приведенной статьей, чтобы узнать, как с помощью портала определить, разрешен или запрещен пакет для конкретной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bad83-116">Visit the following article to learn if a packet is allowed or denied for a specific virtual machine through the portal.</span></span> [<span data-ttu-id="bad83-117">Проверка состояния входящего и исходящего трафика виртуальной машины (разрешен или запрещен) путем проверки IP-потока (компонент Наблюдателя за сетями Azure)</span><span class="sxs-lookup"><span data-stu-id="bad83-117">Check if traffic is allowed on a VM with IP Flow Verify using the portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












