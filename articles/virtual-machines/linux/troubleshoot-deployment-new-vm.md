---
title: "aaaTroubleshoot развертывания виртуальной Машины с Linux-RM | Документы Microsoft"
description: "Устранение неполадок развертывания Resource Manager при создании виртуальной машины Linux в Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="5cf0a-103">Устранение неполадок в развертывании Resource Manager при создании виртуальной машины Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="5cf0a-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="5cf0a-104">Наиболее важные проблемы</span><span class="sxs-lookup"><span data-stu-id="5cf0a-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="5cf0a-105">Описание других ситуаций и вопросов, связанных с развертыванием виртуальных машин, см. в статье [Устранение неполадок при развертывании виртуальных машин Linux в Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="5cf0a-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="5cf0a-106">Сбор журналов действий</span><span class="sxs-lookup"><span data-stu-id="5cf0a-106">Collect activity logs</span></span>
<span data-ttu-id="5cf0a-107">Устранение неполадок, toostart действие сбор hello записывает ошибку tooidentify hello, связанной с проблемой hello.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="5cf0a-108">Hello следующие ссылки содержат подробную информацию по toofollow процесса hello.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="5cf0a-109">Просмотр операций развертывания с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5cf0a-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="5cf0a-110">Просматривать журналы действий toomanage Azure ресурсы</span><span class="sxs-lookup"><span data-stu-id="5cf0a-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="5cf0a-111">**Y:** Если hello ОС Linux обобщены и его отправки и/или записанный с помощью hello обобщенный параметр, то не будет ошибок.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-111">**Y:** If hello OS is Linux generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="5cf0a-112">Аналогично Если hello ОС Linux специализированные и его отправки и/или захватить с hello специализированные параметр, то не будет ошибок.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-112">Similarly, if hello OS is Linux specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="5cf0a-113">**Ошибки передачи:**</span><span class="sxs-lookup"><span data-stu-id="5cf0a-113">**Upload Errors:**</span></span>

<span data-ttu-id="5cf0a-114">**N<sup>1</sup>:** Если hello ОС Linux обобщенный и передается как специализированными, вы получите подготовки ошибку времени ожидания, так как на стадии подготовки hello застряла hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-114">**N<sup>1</sup>:** If hello OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because hello VM is stuck at hello provisioning stage.</span></span>

<span data-ttu-id="5cf0a-115">**N<sup>2</sup>:** Если hello ОС Linux специализированные и отправкой как обобщенный, вы получите инициализации: сбой, так как hello новой виртуальной Машины, выполнив hello исходное имя компьютера, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-115">**N<sup>2</sup>:** If hello OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="5cf0a-116">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="5cf0a-116">**Resolution:**</span></span>

<span data-ttu-id="5cf0a-117">Отправить tooresolve оба эти ошибки Здравствуйте исходного VHD, доступных в локальной среде, с hello же задание, что и для hello ОС (обобщенный/специализированные).</span><span class="sxs-lookup"><span data-stu-id="5cf0a-117">tooresolve both these errors, upload hello original VHD, available on-prem, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="5cf0a-118">tooupload как обобщены, помните toorun-сначала отзыв.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-118">tooupload as generalized, remember toorun -deprovision first.</span></span>

<span data-ttu-id="5cf0a-119">**Ошибки записи:**</span><span class="sxs-lookup"><span data-stu-id="5cf0a-119">**Capture Errors:**</span></span>

<span data-ttu-id="5cf0a-120">**N<sup>3</sup>:** Если hello ОС Linux обобщенный и записывается в виде специализированными, вы получите подготовки ошибка тайм-аута из-за hello исходной виртуальной Машины не может использоваться как она помечена как обобщенный.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-120">**N<sup>3</sup>:** If hello OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="5cf0a-121">**N<sup>4</sup>:** Если специализированные Linux, и она записывается как обобщенный hello операционной системы, вы получите инициализации: сбой, так как hello новой виртуальной Машины, выполнив hello исходное имя компьютера, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-121">**N<sup>4</sup>:** If hello OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span> <span data-ttu-id="5cf0a-122">Кроме того, исходный hello виртуальной Машины не выполняется, так как она помечена как специальные.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="5cf0a-123">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="5cf0a-123">**Resolution:**</span></span>

<span data-ttu-id="5cf0a-124">tooresolve оба эти ошибки удалить текущее изображение hello из портала hello и [захватить снова из hello текущего виртуальные жесткие диски](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) с "hello" того же параметра, что и для hello ОС (обобщенный/специализированные).</span><span class="sxs-lookup"><span data-stu-id="5cf0a-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="5cf0a-125">Проблема: ошибка выделения (пользовательский образ, образ из коллекции или Marketplace)</span><span class="sxs-lookup"><span data-stu-id="5cf0a-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="5cf0a-126">Эта ошибка возникает в ситуациях, при получении новой виртуальной Машины запроса hello закрепленных tooa кластера, либо не поддерживает размер виртуальной Машины hello запрашиваемого, либо не имеет доступного свободного места tooaccommodate hello запроса.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="5cf0a-127">**Причина 1:** hello кластера не поддерживают hello запрошенный размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="5cf0a-128">**Способ устранения 1.**</span><span class="sxs-lookup"><span data-stu-id="5cf0a-128">**Resolution 1:**</span></span>

* <span data-ttu-id="5cf0a-129">Повторите запрос hello, с использованием меньшего размера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="5cf0a-130">Если hello запрошенный размер hello, что виртуальная машина нельзя изменить:</span><span class="sxs-lookup"><span data-stu-id="5cf0a-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="5cf0a-131">Остановите все виртуальные машины hello в наборе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="5cf0a-132">Для этого последовательно выберите **Группы ресурсов** > *имя вашей группы ресурсов* > **Ресурсы** > *имя вашей группы доступности* > **Виртуальные машины** > *имя вашей виртуальной машины* > **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="5cf0a-133">После всех hello остановка виртуальных машин, создайте hello новой виртуальной Машины в hello требуемого размера.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="5cf0a-134">Запустить сначала hello новой виртуальной Машины, а затем выберите каждый hello остановлен, виртуальные машины и нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="5cf0a-135">**Причина 2:** hello кластер не имеет свободных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="5cf0a-136">**Способ устранения 2.**</span><span class="sxs-lookup"><span data-stu-id="5cf0a-136">**Resolution 2:**</span></span>

* <span data-ttu-id="5cf0a-137">Повторите запрос hello позже.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="5cf0a-138">Если hello новой виртуальной Машины можно указать различные доступности</span><span class="sxs-lookup"><span data-stu-id="5cf0a-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="5cf0a-139">Создание новой виртуальной Машины в наборе доступности на другой (в hello одного региона).</span><span class="sxs-lookup"><span data-stu-id="5cf0a-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="5cf0a-140">Добавление новой виртуальной Машины toohello hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="5cf0a-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cf0a-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5cf0a-141">Next steps</span></span>
<span data-ttu-id="5cf0a-142">При возникновении проблем во время запуска остановленной виртуальной машины Linux или в случае изменения размера существующей виртуальной машины Linux в Azure см. раздел [Устранение неполадок в развертывании Resource Manager при перезагрузке или изменении размера существующей виртуальной машины Linux в Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5cf0a-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

