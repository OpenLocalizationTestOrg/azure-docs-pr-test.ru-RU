---
title: "Примеры Azure PowerShell | Документация Майкрософт"
description: "Примеры сценариев Azure PowerShell."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 0bca4fb6874bd265f0ae9faeb4219abeb4ffb6d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="f23ee-103">Примеры Azure PowerShell для работы с сетями</span><span class="sxs-lookup"><span data-stu-id="f23ee-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="f23ee-104">В таблице ниже приведены ссылки на скрипты, созданные с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f23ee-104">The following table includes links to scripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="f23ee-105">**Подключение между ресурсами Azure**</span><span class="sxs-lookup"><span data-stu-id="f23ee-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="f23ee-106">Создание виртуальной сети для многоуровневых приложений</span><span class="sxs-lookup"><span data-stu-id="f23ee-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="f23ee-107">Создание виртуальной сети с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="f23ee-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="f23ee-108">Трафик к интерфейсной подсети принимается по протоколу HTTP, в то время как трафик к внутренней подсети принимается только от SQL через порт 1433.</span><span class="sxs-lookup"><span data-stu-id="f23ee-108">Traffic to the front-end subnet is limited to HTTP, while traffic to the back-end subnet is limited to SQL, port 1433.</span></span> |
| [<span data-ttu-id="f23ee-109">Пиринг между двумя виртуальными сетями</span><span class="sxs-lookup"><span data-stu-id="f23ee-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="f23ee-110">Создание и подключение двух виртуальных сетей в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="f23ee-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="f23ee-111">Маршрутизация трафика через виртуальный сетевой модуль</span><span class="sxs-lookup"><span data-stu-id="f23ee-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="f23ee-112">Создание виртуальной сети с интерфейсной и внутренней подсетями, а также виртуальной машиной, которая может маршрутизировать трафик между этими двумя подсетями.</span><span class="sxs-lookup"><span data-stu-id="f23ee-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="f23ee-113">Фильтрация входящего и исходящего сетевого трафика виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="f23ee-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="f23ee-114">Создание виртуальной сети с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="f23ee-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="f23ee-115">Входящий сетевой трафик в интерфейсной подсети ограничен протоколами HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f23ee-115">Inbound network traffic to the front-end subnet is limited to HTTP and HTTPS..</span></span> <span data-ttu-id="f23ee-116">Исходящий трафик в Интернет из внутренней подсети запрещен.</span><span class="sxs-lookup"><span data-stu-id="f23ee-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="f23ee-117">**Направление трафика и балансировка нагрузки**</span><span class="sxs-lookup"><span data-stu-id="f23ee-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="f23ee-118">Балансировка трафика на виртуальных машинах для обеспечения высокого уровня доступности</span><span class="sxs-lookup"><span data-stu-id="f23ee-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="f23ee-119">Создает несколько виртуальных машин с высокодоступной конфигурацией с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f23ee-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="f23ee-120">Балансировка нагрузки нескольких веб-сайтов на виртуальных машинах</span><span class="sxs-lookup"><span data-stu-id="f23ee-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="f23ee-121">Создание двух виртуальных машин с несколькими IP-конфигурациями, присоединенных к группе доступности Azure, которые доступны через Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="f23ee-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="f23ee-122">Направление трафика через несколько регионов для обеспечения высокого уровня доступности приложений</span><span class="sxs-lookup"><span data-stu-id="f23ee-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="f23ee-123">Создание двух планов службы приложений, двух веб-приложений, а также профиля и двух конечных точек диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="f23ee-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
