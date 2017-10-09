---
title: "Образцы CLI aaaAzure | Документы Microsoft"
description: "Примеры Azure CLI"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="4fe04-103">Примеры Azure CLI для работы с сетью</span><span class="sxs-lookup"><span data-stu-id="4fe04-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="4fe04-104">Hello следующей таблице представлены ссылки toobash сценариев, созданных с использованием hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4fe04-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="4fe04-105">**Подключение между ресурсами Azure**</span><span class="sxs-lookup"><span data-stu-id="4fe04-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="4fe04-106">Создание виртуальной сети для многоуровневых приложений</span><span class="sxs-lookup"><span data-stu-id="4fe04-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="4fe04-107">Создание виртуальной сети с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="4fe04-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="4fe04-108">Подсети интерфейса toohello трафика является ограниченной tooHTTP и SSH, при toohello трафика конечной подсети ограниченный tooMySQL, порт 3306.</span><span class="sxs-lookup"><span data-stu-id="4fe04-108">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> |
| [<span data-ttu-id="4fe04-109">Пиринг между двумя виртуальными сетями</span><span class="sxs-lookup"><span data-stu-id="4fe04-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="4fe04-110">Создается и выполняется подключение двух виртуальных сетей в hello одного региона.</span><span class="sxs-lookup"><span data-stu-id="4fe04-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="4fe04-111">Маршрутизация трафика через виртуальный сетевой модуль</span><span class="sxs-lookup"><span data-stu-id="4fe04-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="4fe04-112">Создает виртуальную сеть с внешнего и внутреннего интерфейса подсети и виртуальной Машины, которое может tooroute трафика между подсетями hello двух.</span><span class="sxs-lookup"><span data-stu-id="4fe04-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="4fe04-113">Фильтрация входящего и исходящего сетевого трафика виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4fe04-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="4fe04-114">Создание виртуальной сети с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="4fe04-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="4fe04-115">Входящий сетевой трафик интерфейса подсеть toohello является ограниченной tooHTTP, HTTPS и SSH.</span><span class="sxs-lookup"><span data-stu-id="4fe04-115">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH.</span></span> <span data-ttu-id="4fe04-116">Исходящий трафик toohello Интернет из внутренней подсети hello не допускается.</span><span class="sxs-lookup"><span data-stu-id="4fe04-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="4fe04-117">**Направление трафика и балансировка нагрузки**</span><span class="sxs-lookup"><span data-stu-id="4fe04-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="4fe04-118">Загрузить tooVMs Балансировка трафика для обеспечения высокой доступности</span><span class="sxs-lookup"><span data-stu-id="4fe04-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="4fe04-119">Создает несколько виртуальных машин с высокодоступной конфигурацией с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4fe04-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="4fe04-120">Балансировка нагрузки нескольких веб-сайтов на виртуальных машинах</span><span class="sxs-lookup"><span data-stu-id="4fe04-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="4fe04-121">Создает две виртуальные машины с несколькими IP-конфигурации, соединенных tooan группе доступности Azure, доступные через подсистемы балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe04-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="4fe04-122">Направление трафика через несколько регионов для обеспечения высокого уровня доступности приложений</span><span class="sxs-lookup"><span data-stu-id="4fe04-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="4fe04-123">Создание двух планов службы приложений, двух веб-приложений, а также профиля и двух конечных точек диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="4fe04-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
