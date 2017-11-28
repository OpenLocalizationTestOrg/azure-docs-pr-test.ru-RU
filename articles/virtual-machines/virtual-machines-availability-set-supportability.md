---
title: "aaaSupportability добавить существующую группу доступности виртуальных машин Azure tooan | Документы Microsoft"
description: "Возможности поддержки добавления виртуальных машин Azure tooan существующую группу доступности."
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
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a><span data-ttu-id="b2da7-103">Возможности поддержки добавления виртуальных машин Azure tooan существующий набор доступности</span><span class="sxs-lookup"><span data-stu-id="b2da7-103">Supportability of adding Azure VMs tooan existing availability set</span></span>

<span data-ttu-id="b2da7-104">Ограничения может столкнуться при добавлении новых виртуальных машин (ВМ) tooan существующую группу доступности.</span><span class="sxs-lookup"><span data-stu-id="b2da7-104">You may occasionally encounter limitations when you add new virtual machines (VMs) tooan existing availability set.</span></span> <span data-ttu-id="b2da7-105">Здравствуйте, приведенные ниже сведения диаграммы Здравствуйте, какому ряду виртуальной Машины, можно сочетать в одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="b2da7-105">hello following chart details which VM series you can mix in hello same availability set.</span></span>

<span data-ttu-id="b2da7-106">Вот hello Матрица поддержки toomix различных типов виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b2da7-106">Here is hello supportability matrix toomix different types of VMs:</span></span>

<span data-ttu-id="b2da7-107">Серии и группа доступности</span><span class="sxs-lookup"><span data-stu-id="b2da7-107">Series & Availability Set</span></span>|<span data-ttu-id="b2da7-108">Вторая виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="b2da7-108">Second VM</span></span>|<span data-ttu-id="b2da7-109">Файл ,</span><span class="sxs-lookup"><span data-stu-id="b2da7-109">A</span></span>|<span data-ttu-id="b2da7-110">Av2</span><span class="sxs-lookup"><span data-stu-id="b2da7-110">Av2</span></span>|<span data-ttu-id="b2da7-111">D</span><span class="sxs-lookup"><span data-stu-id="b2da7-111">D</span></span>|<span data-ttu-id="b2da7-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="b2da7-112">Dv2</span></span>|<span data-ttu-id="b2da7-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="b2da7-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="b2da7-114">Первая виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="b2da7-114">First VM</span></span>|||||||
|<span data-ttu-id="b2da7-115">Файл ,</span><span class="sxs-lookup"><span data-stu-id="b2da7-115">A</span></span>||<span data-ttu-id="b2da7-116">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-116">OK</span></span>|<span data-ttu-id="b2da7-117">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-117">OK</span></span>|<span data-ttu-id="b2da7-118">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-118">OK</span></span>|<span data-ttu-id="b2da7-119">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-119">OK</span></span>|<span data-ttu-id="b2da7-120">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-120">OK</span></span>|
|<span data-ttu-id="b2da7-121">Av2</span><span class="sxs-lookup"><span data-stu-id="b2da7-121">Av2</span></span>||<span data-ttu-id="b2da7-122">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-122">OK</span></span>|<span data-ttu-id="b2da7-123">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-123">OK</span></span>|<span data-ttu-id="b2da7-124">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-124">OK</span></span>|<span data-ttu-id="b2da7-125">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-125">OK</span></span>|<span data-ttu-id="b2da7-126">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-126">OK</span></span>|
|<span data-ttu-id="b2da7-127">D</span><span class="sxs-lookup"><span data-stu-id="b2da7-127">D</span></span>||<span data-ttu-id="b2da7-128">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-128">OK</span></span>|<span data-ttu-id="b2da7-129">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-129">OK</span></span>|<span data-ttu-id="b2da7-130">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-130">OK</span></span>|<span data-ttu-id="b2da7-131">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-131">OK</span></span>|<span data-ttu-id="b2da7-132">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-132">OK</span></span>|
|<span data-ttu-id="b2da7-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="b2da7-133">Dv2</span></span>||<span data-ttu-id="b2da7-134">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-134">OK</span></span>|<span data-ttu-id="b2da7-135">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-135">OK</span></span>|<span data-ttu-id="b2da7-136">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-136">OK</span></span>|<span data-ttu-id="b2da7-137">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-137">OK</span></span>|<span data-ttu-id="b2da7-138">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-138">OK</span></span>|
|<span data-ttu-id="b2da7-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="b2da7-139">Dv3</span></span>||<span data-ttu-id="b2da7-140">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-140">OK</span></span>|<span data-ttu-id="b2da7-141">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-141">OK</span></span>|<span data-ttu-id="b2da7-142">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-142">OK</span></span>|<span data-ttu-id="b2da7-143">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-143">OK</span></span>|<span data-ttu-id="b2da7-144">ОК</span><span class="sxs-lookup"><span data-stu-id="b2da7-144">OK</span></span>|

<span data-ttu-id="b2da7-145">Все ряды не могут содержаться в hello набор же доступности, так как они требуют определенного оборудования.</span><span class="sxs-lookup"><span data-stu-id="b2da7-145">All other series could not be in hello same availability set because they require a specific hardware.</span></span>
