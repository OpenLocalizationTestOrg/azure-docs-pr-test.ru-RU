---
title: "Примеры PowerShell aaaAzure | Документы Microsoft"
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
ms.openlocfilehash: 130a6e755691b46a9549cad5acaa5bde4fe38e95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="a463c-103">Примеры Azure PowerShell для работы с сетями</span><span class="sxs-lookup"><span data-stu-id="a463c-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="a463c-104">Hello приведенной ниже таблице указаны ссылки tooscripts, созданного с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a463c-104">hello following table includes links tooscripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="a463c-105">**Подключение между ресурсами Azure**</span><span class="sxs-lookup"><span data-stu-id="a463c-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="a463c-106">Создание виртуальной сети для многоуровневых приложений</span><span class="sxs-lookup"><span data-stu-id="a463c-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="a463c-107">Создание виртуальной сети с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="a463c-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="a463c-108">Подсети интерфейса toohello трафика ограниченный tooHTTP, при toohello трафика конечной подсети ограниченный tooSQL, порт 1433.</span><span class="sxs-lookup"><span data-stu-id="a463c-108">Traffic toohello front-end subnet is limited tooHTTP, while traffic toohello back-end subnet is limited tooSQL, port 1433.</span></span> |
| [<span data-ttu-id="a463c-109">Пиринг между двумя виртуальными сетями</span><span class="sxs-lookup"><span data-stu-id="a463c-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="a463c-110">Создается и выполняется подключение двух виртуальных сетей в hello одного региона.</span><span class="sxs-lookup"><span data-stu-id="a463c-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="a463c-111">Маршрутизация трафика через виртуальный сетевой модуль</span><span class="sxs-lookup"><span data-stu-id="a463c-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="a463c-112">Создает виртуальную сеть с внешнего и внутреннего интерфейса подсети и виртуальной Машины, которое может tooroute трафика между подсетями hello двух.</span><span class="sxs-lookup"><span data-stu-id="a463c-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="a463c-113">Фильтрация входящего и исходящего сетевого трафика виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="a463c-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="a463c-114">Создание виртуальной сети с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="a463c-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="a463c-115">Входящий сетевой трафик интерфейса подсеть toohello является ограниченной tooHTTP и HTTPS...</span><span class="sxs-lookup"><span data-stu-id="a463c-115">Inbound network traffic toohello front-end subnet is limited tooHTTP and HTTPS..</span></span> <span data-ttu-id="a463c-116">Исходящий трафик toohello Интернет из внутренней подсети hello не допускается.</span><span class="sxs-lookup"><span data-stu-id="a463c-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="a463c-117">**Направление трафика и балансировка нагрузки**</span><span class="sxs-lookup"><span data-stu-id="a463c-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="a463c-118">Загрузить tooVMs Балансировка трафика для обеспечения высокой доступности</span><span class="sxs-lookup"><span data-stu-id="a463c-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="a463c-119">Создает несколько виртуальных машин с высокодоступной конфигурацией с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a463c-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="a463c-120">Балансировка нагрузки нескольких веб-сайтов на виртуальных машинах</span><span class="sxs-lookup"><span data-stu-id="a463c-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="a463c-121">Создает две виртуальные машины с несколькими IP-конфигурации, соединенных tooan группе доступности Azure, доступные через подсистемы балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="a463c-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="a463c-122">Направление трафика через несколько регионов для обеспечения высокого уровня доступности приложений</span><span class="sxs-lookup"><span data-stu-id="a463c-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="a463c-123">Создание двух планов службы приложений, двух веб-приложений, а также профиля и двух конечных точек диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="a463c-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
