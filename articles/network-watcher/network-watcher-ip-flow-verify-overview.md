---
title: "проверить aaaIntroduction tooIP потока в Наблюдатель сети Azure | Документы Microsoft"
description: "Эта страница предоставляет обзор потока hello наблюдателя сетевого IP-адреса, убедитесь в возможности"
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
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="db06d-103">Проверить поток tooIP введение в Наблюдатель сети Azure</span><span class="sxs-lookup"><span data-stu-id="db06d-103">Introduction tooIP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="db06d-104">Если пакет разрешен или запрещен tooor из виртуальной машины на основе сведений 5-фрагментному IP потока проверьте проверок.</span><span class="sxs-lookup"><span data-stu-id="db06d-104">IP flow verify checks if a packet is allowed or denied tooor from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="db06d-105">Эта информация включает в себя направление, протокол, локальный IP-адрес, удаленный IP-адрес, локальный порт и удаленный порт.</span><span class="sxs-lookup"><span data-stu-id="db06d-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="db06d-106">Если пакет приветствия запрещен группой безопасности, возвращается имя hello hello правила, которое запрещено пакет приветствия.</span><span class="sxs-lookup"><span data-stu-id="db06d-106">If hello packet is denied by a security group, hello name of hello rule that denied hello packet is returned.</span></span> <span data-ttu-id="db06d-107">Хотя можно выбрать любой источник или назначение IP-адрес, эта функция позволяет администраторам быстро найти причину проблем с подключением из или toohello Интернет и из или toohello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="db06d-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or toohello internet and from or toohello on-premises environment.</span></span>

<span data-ttu-id="db06d-108">Функция проверки IP-потока нацеливается на сетевой интерфейс виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="db06d-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="db06d-109">Поток трафика затем проверяются зависимости tooor hello настроены параметры из этот сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="db06d-109">Traffic flow is then verified based on hello configured settings tooor from that network interface.</span></span> <span data-ttu-id="db06d-110">Эта возможность полезна в подтверждении, блокирует ли правила в группе безопасности сети tooor трафик входящих и исходящих из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="db06d-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic tooor from a virtual machine.</span></span>

<span data-ttu-id="db06d-111">Проверка экземпляра toobe потребностей Наблюдатель сети, созданные во всех регионах, планировании toorun IP потока.</span><span class="sxs-lookup"><span data-stu-id="db06d-111">An instance of Network Watcher needs toobe created in all regions that you plan toorun IP flow verify.</span></span> <span data-ttu-id="db06d-112">Наблюдатель сети является региональные службы и может быть выполняли только для ресурсов в hello одного региона.</span><span class="sxs-lookup"><span data-stu-id="db06d-112">Network Watcher is a regional service and can only be ran against resources in hello same region.</span></span> <span data-ttu-id="db06d-113">Это не влияет на результаты IP потока убедитесь в том, как hello маршрута, связанного с сетевой Адаптер будет возвращаться приветствия hello.</span><span class="sxs-lookup"><span data-stu-id="db06d-113">This does not affect hello results of IP flow verify as hello route associated with hello NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="db06d-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="db06d-115">Next steps</span></span>

<span data-ttu-id="db06d-116">Посетите следующие toolearn статьи, если пакет разрешен или запрещен для конкретной виртуальной машины через портал hello hello.</span><span class="sxs-lookup"><span data-stu-id="db06d-116">Visit hello following article toolearn if a packet is allowed or denied for a specific virtual machine through hello portal.</span></span> [<span data-ttu-id="db06d-117">Проверьте, если трафик на виртуальную Машину с IP потока убедитесь с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="db06d-117">Check if traffic is allowed on a VM with IP Flow Verify using hello portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












