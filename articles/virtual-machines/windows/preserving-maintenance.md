---
title: "Обслуживание с сохранением для виртуальных машин Windows в Azure | Документация Майкрософт"
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
ms.openlocfilehash: 8888bafbc3aba24168312b611a9b4fbde25f376d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a><span data-ttu-id="34305-103">Обслуживание с сохранением виртуальной машины посредством миграции на месте</span><span class="sxs-lookup"><span data-stu-id="34305-103">VM preserving maintenance with In-place VM migration</span></span>

<span data-ttu-id="34305-104">Хотя большинство обновлений не влияет на размещенные виртуальные машины, в некоторых случаях обновления компонентов или служб приводят к минимальным помехам в работе виртуальных машин (без их полной перезагрузки).</span><span class="sxs-lookup"><span data-stu-id="34305-104">While the majority of updates have no impact to hosted VMs, there are cases where updates to components or services result in minimal interference to running VMs (without a full reboot of the virtual machine).</span></span>

<span data-ttu-id="34305-105">Эти обновления выполняются с помощью технологии, позволяющей использовать динамическую миграцию на месте (т. н. "обновление с сохранением памяти").</span><span class="sxs-lookup"><span data-stu-id="34305-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="34305-106">При обновлении узла виртуальная машина переводится в состояние приостановки, сохраняя содержимое памяти в ОЗУ, пока среда размещения (т. е. базовая операционная система) применяет необходимые обновления и исправления.</span><span class="sxs-lookup"><span data-stu-id="34305-106">When updating the host, the virtual machine is placed into a “paused” state, preserving the memory in RAM, while the hosting environment (e.g. the underlying operating system) applies the necessary updates and patches.</span></span>
<span data-ttu-id="34305-107">Виртуальная машина возобновляет работу в течение 30 секунд с момента ее приостановки.</span><span class="sxs-lookup"><span data-stu-id="34305-107">The virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="34305-108">После возобновления работы часы виртуальной машины автоматически синхронизируются.</span><span class="sxs-lookup"><span data-stu-id="34305-108">After resuming, the clock of the virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="34305-109">Не все обновления можно развернуть с помощью этого механизма, но благодаря короткому периоду приостановки такой способ развертывания обновлений значительно уменьшает влияние на виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="34305-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact to virtual machines.</span></span>

<span data-ttu-id="34305-110">Обновления для нескольких экземпляров (для виртуальных машин в группе доступности) применяются для одного домена обновления за раз.</span><span class="sxs-lookup"><span data-stu-id="34305-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="34305-111">Эти обновления могут влиять на одни приложения больше, чем на другие.</span><span class="sxs-lookup"><span data-stu-id="34305-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="34305-112">Например, приложения, которые выполняют обработку событий в реальном времени, перекодирование или потоковую передачу мультимедиа либо требуют высокой пропускной способности, не могут допускать 30-секундную паузу.</span><span class="sxs-lookup"><span data-stu-id="34305-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed to tolerate a 30 second pause.</span></span> <span data-ttu-id="34305-113">Приложения, запущенные на виртуальной машине, могут узнавать о предстоящих обновлениях, вызывая API [запланированных событий](../virtual-machines-scheduled-events.md) [службы метаданных Azure](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34305-113">Applications running in a virtual machine can learn about upcoming updates by calling the [Scheduled Events](../virtual-machines-scheduled-events.md) API of the [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
