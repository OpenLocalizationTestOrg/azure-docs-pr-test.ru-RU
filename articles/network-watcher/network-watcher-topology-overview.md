---
title: "tootopology aaaIntroduction в Наблюдатель сети Azure | Документы Microsoft"
description: "Эта страница предоставляет обзор возможностей топологии hello Наблюдатель сети"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a><span data-ttu-id="59a89-103">Tootopology введение в инспектор сети Azure</span><span class="sxs-lookup"><span data-stu-id="59a89-103">Introduction tootopology in Azure Network Watcher</span></span>

<span data-ttu-id="59a89-104">Топология возвращает граф сетевых ресурсов в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="59a89-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="59a89-105">Hello диаграмма показывает hello взаимосвязь между hello ресурсы toorepresent hello окончания tooend сетевое подключение.</span><span class="sxs-lookup"><span data-stu-id="59a89-105">hello graph depicts hello interconnection between hello resources toorepresent hello end tooend network connectivity.</span></span>

![Обзор топологии][1]

<span data-ttu-id="59a89-107">В портал hello топологии возвращает hello объектов ресурсов для каждой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="59a89-107">In hello portal, Topology returns hello resource objects on a per virtual network basis.</span></span> <span data-ttu-id="59a89-108">связи Hello изображаются линиями между hello ресурсы за пределами области hello Наблюдатель сети, даже если в hello ресурсов группы не отображается.</span><span class="sxs-lookup"><span data-stu-id="59a89-108">hello relationships are depicted by lines between hello resources Resources outside of hello Network Watcher region, even if in hello resource group will not be displayed.</span></span> <span data-ttu-id="59a89-109">ресурсы Hello, возвращаемые в представлении портала hello представляют собой подмножество hello сетевых компонентов, отображаемых в графике.</span><span class="sxs-lookup"><span data-stu-id="59a89-109">hello resources returned in hello portal view are a subset of hello networking components that are graphed.</span></span> <span data-ttu-id="59a89-110">toosee hello полный список сетевых ресурсов можно использовать [PowerShell](network-watcher-topology-powershell.md) или [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="59a89-110">toosee hello full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="59a89-111">Требуется экземпляр Наблюдатель сети в каждом регионе нужного toorun топологии.</span><span class="sxs-lookup"><span data-stu-id="59a89-111">An instance of Network Watcher is required in each region that you want toorun Topology on.</span></span>

<span data-ttu-id="59a89-112">В разделе две связи моделируются как ресурсы возвращаются hello соединения между ними.</span><span class="sxs-lookup"><span data-stu-id="59a89-112">As resources are returned hello connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="59a89-113">**Вложение.** Например, виртуальная сеть содержит подсеть, которая, в свою очередь, содержит сетевую карту.</span><span class="sxs-lookup"><span data-stu-id="59a89-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="59a89-114">**Связь.** Например, сетевая карта связана с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="59a89-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="59a89-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59a89-115">Next steps</span></span>

<span data-ttu-id="59a89-116">Узнайте, как просмотреть toouse PowerShell tooretrieve hello топологии, посетив [топологией Наблюдатель сети с помощью PowerShell](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="59a89-116">Learn how toouse PowerShell tooretrieve hello Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
