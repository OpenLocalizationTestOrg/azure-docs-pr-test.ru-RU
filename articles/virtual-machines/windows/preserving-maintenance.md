---
title: "AAA обслуживания сохранения виртуальной Машины для виртуальных машин Windows в Azure | Документы Microsoft"
description: "Миграция виртуальной машины на месте для обновлений с сохранением содержимого памяти."
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: b798f0afd9d8dc60ca8a78f7cc77435a0ddc76fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a><span data-ttu-id="fbcc9-103">Обслуживание с сохранением виртуальной машины посредством миграции на месте</span><span class="sxs-lookup"><span data-stu-id="fbcc9-103">VM preserving maintenance with In-place VM migration</span></span>

<span data-ttu-id="fbcc9-104">Хотя hello большинство обновлений не влияние toohosted виртуальных машин, существуют случаи, когда toocomponents обновления или службы привести toorunning минимальной помех виртуальных машин (без полной перезагрузки hello виртуальной машины).</span><span class="sxs-lookup"><span data-stu-id="fbcc9-104">While hello majority of updates have no impact toohosted VMs, there are cases where updates toocomponents or services result in minimal interference toorunning VMs (without a full reboot of hello virtual machine).</span></span>

<span data-ttu-id="fbcc9-105">Эти обновления выполняются с помощью технологии, позволяющей использовать динамическую миграцию на месте (т. н. "обновление с сохранением памяти").</span><span class="sxs-lookup"><span data-stu-id="fbcc9-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="fbcc9-106">При обновлении узла hello, hello виртуальная машина размещена в состояние «приостановлена», сохраняя памяти hello в оперативной памяти, а hello (например операционной системы) среда размещения применяется hello необходимых обновлений и исправлений.</span><span class="sxs-lookup"><span data-stu-id="fbcc9-106">When updating hello host, hello virtual machine is placed into a “paused” state, preserving hello memory in RAM, while hello hosting environment (e.g. the underlying operating system) applies hello necessary updates and patches.</span></span>
<span data-ttu-id="fbcc9-107">Hello виртуальной машины, затем будет возобновлена в течение 30 секунд для приостановки.</span><span class="sxs-lookup"><span data-stu-id="fbcc9-107">hello virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="fbcc9-108">После возобновления автоматической синхронизации часов hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fbcc9-108">After resuming, hello clock of hello virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="fbcc9-109">Не все обновления можно развернуть с помощью этого механизма, но заданного периода короче, значительно способом развертывания обновлений в это уменьшает влияние toovirtual машины.</span><span class="sxs-lookup"><span data-stu-id="fbcc9-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact toovirtual machines.</span></span>

<span data-ttu-id="fbcc9-110">Обновления для нескольких экземпляров (для виртуальных машин в группе доступности) применяются для одного домена обновления за раз.</span><span class="sxs-lookup"><span data-stu-id="fbcc9-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="fbcc9-111">Эти обновления могут влиять на одни приложения больше, чем на другие.</span><span class="sxs-lookup"><span data-stu-id="fbcc9-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="fbcc9-112">Приложения, которые выполняют обработки событий в реальном времени, потоковой передачи мультимедиа или перекодирования или высокой пропускной способностью сети сценариев, например, может оказаться спроектированный tootolerate 30 секундной паузы.</span><span class="sxs-lookup"><span data-stu-id="fbcc9-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed tootolerate a 30 second pause.</span></span> <span data-ttu-id="fbcc9-113">Приложения, работающие на виртуальной машине узнать о предстоящих обновлениях, вызывающему Привет [запланированные события](../virtual-machines-scheduled-events.md) API-Интерфейс hello [службы метаданных Azure](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbcc9-113">Applications running in a virtual machine can learn about upcoming updates by calling hello [Scheduled Events](../virtual-machines-scheduled-events.md) API of hello [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
