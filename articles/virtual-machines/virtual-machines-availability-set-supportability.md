---
title: "Поддержка добавления виртуальных машин Azure в существующую группу доступности | Документы Майкрософт"
description: "Поддержка добавления виртуальных машин Azure в существующую группу доступности."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: 3ce9b8a79108cb9e57df14bcb3354cc637193233
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="supportability-of-adding-azure-vms-to-an-existing-availability-set"></a><span data-ttu-id="27f10-103">Поддержка добавления виртуальных машин Azure в существующую группу доступности</span><span class="sxs-lookup"><span data-stu-id="27f10-103">Supportability of adding Azure VMs to an existing availability set</span></span>

<span data-ttu-id="27f10-104">Иногда вы можете столкнуться с ограничениями при добавлении новых виртуальных машин в существующую группу доступности.</span><span class="sxs-lookup"><span data-stu-id="27f10-104">You may occasionally encounter limitations when you add new virtual machines (VMs) to an existing availability set.</span></span> <span data-ttu-id="27f10-105">На следующей диаграмме показано, какие серии виртуальных машин можно объединить в одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="27f10-105">The following chart details which VM series you can mix in the same availability set.</span></span>

<span data-ttu-id="27f10-106">Ниже приводится матрица поддержки для объединения различных типов виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="27f10-106">Here is the supportability matrix to mix different types of VMs:</span></span>

<span data-ttu-id="27f10-107">Серии и группа доступности</span><span class="sxs-lookup"><span data-stu-id="27f10-107">Series & Availability Set</span></span>|<span data-ttu-id="27f10-108">Вторая виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="27f10-108">Second VM</span></span>|<span data-ttu-id="27f10-109">Файл ,</span><span class="sxs-lookup"><span data-stu-id="27f10-109">A</span></span>|<span data-ttu-id="27f10-110">Av2</span><span class="sxs-lookup"><span data-stu-id="27f10-110">Av2</span></span>|<span data-ttu-id="27f10-111">D</span><span class="sxs-lookup"><span data-stu-id="27f10-111">D</span></span>|<span data-ttu-id="27f10-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="27f10-112">Dv2</span></span>|<span data-ttu-id="27f10-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="27f10-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="27f10-114">Первая виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="27f10-114">First VM</span></span>|||||||
|<span data-ttu-id="27f10-115">Файл ,</span><span class="sxs-lookup"><span data-stu-id="27f10-115">A</span></span>||<span data-ttu-id="27f10-116">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-116">OK</span></span>|<span data-ttu-id="27f10-117">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-117">OK</span></span>|<span data-ttu-id="27f10-118">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-118">OK</span></span>|<span data-ttu-id="27f10-119">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-119">OK</span></span>|<span data-ttu-id="27f10-120">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-120">OK</span></span>|
|<span data-ttu-id="27f10-121">Av2</span><span class="sxs-lookup"><span data-stu-id="27f10-121">Av2</span></span>||<span data-ttu-id="27f10-122">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-122">OK</span></span>|<span data-ttu-id="27f10-123">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-123">OK</span></span>|<span data-ttu-id="27f10-124">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-124">OK</span></span>|<span data-ttu-id="27f10-125">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-125">OK</span></span>|<span data-ttu-id="27f10-126">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-126">OK</span></span>|
|<span data-ttu-id="27f10-127">D</span><span class="sxs-lookup"><span data-stu-id="27f10-127">D</span></span>||<span data-ttu-id="27f10-128">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-128">OK</span></span>|<span data-ttu-id="27f10-129">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-129">OK</span></span>|<span data-ttu-id="27f10-130">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-130">OK</span></span>|<span data-ttu-id="27f10-131">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-131">OK</span></span>|<span data-ttu-id="27f10-132">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-132">OK</span></span>|
|<span data-ttu-id="27f10-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="27f10-133">Dv2</span></span>||<span data-ttu-id="27f10-134">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-134">OK</span></span>|<span data-ttu-id="27f10-135">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-135">OK</span></span>|<span data-ttu-id="27f10-136">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-136">OK</span></span>|<span data-ttu-id="27f10-137">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-137">OK</span></span>|<span data-ttu-id="27f10-138">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-138">OK</span></span>|
|<span data-ttu-id="27f10-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="27f10-139">Dv3</span></span>||<span data-ttu-id="27f10-140">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-140">OK</span></span>|<span data-ttu-id="27f10-141">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-141">OK</span></span>|<span data-ttu-id="27f10-142">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-142">OK</span></span>|<span data-ttu-id="27f10-143">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-143">OK</span></span>|<span data-ttu-id="27f10-144">ОК</span><span class="sxs-lookup"><span data-stu-id="27f10-144">OK</span></span>|

<span data-ttu-id="27f10-145">Все остальные серии не могут находиться в одной и той же группе доступности, так как для них требуется определенное оборудование.</span><span class="sxs-lookup"><span data-stu-id="27f10-145">All other series could not be in the same availability set because they require a specific hardware.</span></span>