---
title: "aaaMicrosoft архитектура пакета средств разработки стек Azure | Документы Microsoft"
description: "Здравствуйте, представление архитектуры пакета средств разработки Microsoft Azure стека."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: helaw
ms.openlocfilehash: 32a19ced7ddd57b97ba796679c116132090402e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-stack-development-kit-architecture"></a><span data-ttu-id="e9558-103">Архитектура пакета средств разработки Microsoft Azure стека</span><span class="sxs-lookup"><span data-stu-id="e9558-103">Microsoft Azure Stack Development Kit architecture</span></span>
<span data-ttu-id="e9558-104">Hello пакет средств разработки стек Azure — это развертывание одного узла Azure стека.</span><span class="sxs-lookup"><span data-stu-id="e9558-104">hello Azure Stack Development Kit is a single-node deployment of Azure Stack.</span></span> <span data-ttu-id="e9558-105">Все компоненты hello устанавливаются в виртуальных машин, работающих на одном хост-компьютере.</span><span class="sxs-lookup"><span data-stu-id="e9558-105">All hello components are installed in virtual machines running on a single host machine.</span></span> 

## <a name="logical-architecture-diagram"></a><span data-ttu-id="e9558-106">Диаграмма логической архитектуры</span><span class="sxs-lookup"><span data-stu-id="e9558-106">Logical architecture diagram</span></span>
<span data-ttu-id="e9558-107">Hello следующей схеме показана логическая архитектура hello пакет средств разработки Azure стека hello и его компонентов.</span><span class="sxs-lookup"><span data-stu-id="e9558-107">hello following diagram illustrates hello logical architecture of hello Azure Stack development kit and its components.</span></span>

![](media/azure-stack-architecture/image1.png)

## <a name="virtual-machine-roles"></a><span data-ttu-id="e9558-108">Роли виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e9558-108">Virtual machine roles</span></span>
<span data-ttu-id="e9558-109">Hello пакет средств разработки стек Azure предлагает службы, с помощью следующих виртуальных машин на узле hello hello:</span><span class="sxs-lookup"><span data-stu-id="e9558-109">hello Azure Stack development kit offers services using hello following VMs on hello host:</span></span>

| <span data-ttu-id="e9558-110">Имя</span><span class="sxs-lookup"><span data-stu-id="e9558-110">Name</span></span> | <span data-ttu-id="e9558-111">Описание</span><span class="sxs-lookup"><span data-stu-id="e9558-111">Description</span></span> |
| ----- | ----- |
| <span data-ttu-id="e9558-112">**AzS ACS01**</span><span class="sxs-lookup"><span data-stu-id="e9558-112">**AzS-ACS01**</span></span> | <span data-ttu-id="e9558-113">Службы хранилища Azure стека.</span><span class="sxs-lookup"><span data-stu-id="e9558-113">Azure Stack storage services.</span></span>|
| <span data-ttu-id="e9558-114">**AzS ADFS01**</span><span class="sxs-lookup"><span data-stu-id="e9558-114">**AzS-ADFS01**</span></span> | <span data-ttu-id="e9558-115">Службы федерации Active Directory (ADFS).</span><span class="sxs-lookup"><span data-stu-id="e9558-115">Active Directory Federation Services (ADFS).</span></span>  |
| <span data-ttu-id="e9558-116">**AzS BGPNAT01**</span><span class="sxs-lookup"><span data-stu-id="e9558-116">**AzS-BGPNAT01**</span></span> | <span data-ttu-id="e9558-117">Пограничный маршрутизатор и предоставляет возможности NAT и VPN Azure стека.</span><span class="sxs-lookup"><span data-stu-id="e9558-117">Edge router and provides NAT and VPN capabilities for Azure Stack.</span></span> |
| <span data-ttu-id="e9558-118">**AzS CA01**</span><span class="sxs-lookup"><span data-stu-id="e9558-118">**AzS-CA01**</span></span> | <span data-ttu-id="e9558-119">Службы сертификатов центр служб ролей Azure стека.</span><span class="sxs-lookup"><span data-stu-id="e9558-119">Certificate authority services for Azure Stack role services.</span></span>|
| <span data-ttu-id="e9558-120">**AzS DC01**</span><span class="sxs-lookup"><span data-stu-id="e9558-120">**AzS-DC01**</span></span> | <span data-ttu-id="e9558-121">Active Directory, DNS и DHCP-службы для стека Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e9558-121">Active Directory, DNS, and DHCP services for Microsoft Azure Stack.</span></span>|
| <span data-ttu-id="e9558-122">**AzS ERCS01**</span><span class="sxs-lookup"><span data-stu-id="e9558-122">**AzS-ERCS01**</span></span> | <span data-ttu-id="e9558-123">Консоль аварийного восстановления виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e9558-123">Emergency Recovery Console VM.</span></span> |
| <span data-ttu-id="e9558-124">**AzS GWY01**</span><span class="sxs-lookup"><span data-stu-id="e9558-124">**AzS-GWY01**</span></span> | <span data-ttu-id="e9558-125">Шлюз служб как VPN-подключения сеть сеть для сетей клиентов.</span><span class="sxs-lookup"><span data-stu-id="e9558-125">Edge gateway services such as VPN site-to-site connections for tenant networks.</span></span>|
| <span data-ttu-id="e9558-126">**AzS NC01**</span><span class="sxs-lookup"><span data-stu-id="e9558-126">**AzS-NC01**</span></span> | <span data-ttu-id="e9558-127">Сетевой контроллер управляет службами сетевой стек Azure.</span><span class="sxs-lookup"><span data-stu-id="e9558-127">Network Controller, which manages Azure Stack network services.</span></span>  |
| <span data-ttu-id="e9558-128">**AzS SLB01**</span><span class="sxs-lookup"><span data-stu-id="e9558-128">**AzS-SLB01**</span></span> | <span data-ttu-id="e9558-129">Балансировка нагрузки мультиплексор служб Azure стека для клиентов и служб инфраструктуры Azure стека.</span><span class="sxs-lookup"><span data-stu-id="e9558-129">Load balancing multiplexer services in Azure Stack for both tenants and Azure Stack infrastructure services.</span></span>  |
| <span data-ttu-id="e9558-130">**AzS SQL01**</span><span class="sxs-lookup"><span data-stu-id="e9558-130">**AzS-SQL01**</span></span> | <span data-ttu-id="e9558-131">Для ролей инфраструктуры Azure стека хранения внутренних данных.</span><span class="sxs-lookup"><span data-stu-id="e9558-131">Internal data store for Azure Stack infrastructure roles.</span></span>  |
| <span data-ttu-id="e9558-132">**AzS WAS01**</span><span class="sxs-lookup"><span data-stu-id="e9558-132">**AzS-WAS01**</span></span> | <span data-ttu-id="e9558-133">Службы диспетчера ресурсов Azure и портала администрирования Azure стека.</span><span class="sxs-lookup"><span data-stu-id="e9558-133">Azure Stack administrative portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="e9558-134">**AzS WASP01**</span><span class="sxs-lookup"><span data-stu-id="e9558-134">**AzS-WASP01**</span></span>| <span data-ttu-id="e9558-135">Стек пользователя (клиент) Azure и службы диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="e9558-135">Azure Stack user (tenant) portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="e9558-136">**AzS XRP01**</span><span class="sxs-lookup"><span data-stu-id="e9558-136">**AzS-XRP01**</span></span> | <span data-ttu-id="e9558-137">Контроллер управления инфраструктуры для стека Microsoft Azure, включая hello поставщики ресурсов вычисления, сети и хранилища.</span><span class="sxs-lookup"><span data-stu-id="e9558-137">Infrastructure management controller for Microsoft Azure Stack, including hello Compute, Network, and Storage resource providers.</span></span>|


## <a name="next-steps"></a><span data-ttu-id="e9558-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e9558-138">Next steps</span></span>
[<span data-ttu-id="e9558-139">Развертывание стек Azure</span><span class="sxs-lookup"><span data-stu-id="e9558-139">Deploy Azure Stack</span></span>](azure-stack-deploy.md)

[<span data-ttu-id="e9558-140">Первый tootry сценариев</span><span class="sxs-lookup"><span data-stu-id="e9558-140">First scenarios tootry</span></span>](azure-stack-first-scenarios.md)

