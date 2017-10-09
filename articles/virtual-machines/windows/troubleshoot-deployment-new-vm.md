---
title: "aaaTroubleshoot развертывание виртуальной Машины Windows в Azure | Документы Microsoft"
description: "Устранение неполадок развертывания Resource Manager при создании виртуальной машины Windows в Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c27d4f63b67db2d1c9f117f05a2eba9ef130ef37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a><span data-ttu-id="7db4d-103">Устранение неполадок развертывания при создании виртуальной машины Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="7db4d-103">Troubleshoot deployment issues when creating a new Windows VM in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="7db4d-104">Наиболее важные проблемы</span><span class="sxs-lookup"><span data-stu-id="7db4d-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="7db4d-105">Описание других ситуаций и вопросов, связанных с развертыванием виртуальных машин, см. в статье [Устранение неполадок при развертывании виртуальных машин Windows в Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="7db4d-105">For other VM deployment issues and questions, see [Troubleshoot deploying Windows virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>

## <a name="collect-activity-logs"></a><span data-ttu-id="7db4d-106">Сбор журналов действий</span><span class="sxs-lookup"><span data-stu-id="7db4d-106">Collect activity logs</span></span>
<span data-ttu-id="7db4d-107">Устранение неполадок, toostart действие сбор hello записывает ошибку tooidentify hello, связанной с проблемой hello.</span><span class="sxs-lookup"><span data-stu-id="7db4d-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="7db4d-108">Hello следующие ссылки содержат подробную информацию по toofollow процесса hello.</span><span class="sxs-lookup"><span data-stu-id="7db4d-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="7db4d-109">Просмотр операций развертывания с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7db4d-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="7db4d-110">Просматривать журналы действий toomanage Azure ресурсы</span><span class="sxs-lookup"><span data-stu-id="7db4d-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="7db4d-111">**Y:** Если hello ОС Windows обобщены и его отправки и/или записанный с помощью hello обобщенный параметр, то не будет ошибок.</span><span class="sxs-lookup"><span data-stu-id="7db4d-111">**Y:** If hello OS is Windows generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="7db4d-112">Аналогично Если hello ОС специализированные Windows, и его отправки и/или захватить с hello специализированные параметр, то не будет ошибок.</span><span class="sxs-lookup"><span data-stu-id="7db4d-112">Similarly, if hello OS is Windows specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="7db4d-113">**Ошибки передачи:**</span><span class="sxs-lookup"><span data-stu-id="7db4d-113">**Upload Errors:**</span></span>

<span data-ttu-id="7db4d-114">**N<sup>1</sup>:** Если hello ОС Windows обобщенный и передается как специализированными, возникнет ошибка подготовки тайм-аута с виртуальной Машины заблокировано на экране Приветствия hello hello.</span><span class="sxs-lookup"><span data-stu-id="7db4d-114">**N<sup>1</sup>:** If hello OS is Windows generalized, and it is uploaded as specialized, you will get a provisioning timeout error with hello VM stuck at hello OOBE screen.</span></span>

<span data-ttu-id="7db4d-115">**N<sup>2</sup>:** Если hello ОС Windows специализированные и отправкой как обобщенный, вы получите подготовки ошибка с виртуальной Машины заблокировано на экран Приветствия hello, поскольку hello Новая виртуальная машина запущена с исходного компьютера hello hello имя, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="7db4d-115">**N<sup>2</sup>:** If hello OS is Windows specialized, and it is uploaded as generalized, you will get a provisioning failure error with hello VM stuck at hello OOBE screen because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="7db4d-116">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="7db4d-116">**Resolution**</span></span>

<span data-ttu-id="7db4d-117">использовать оба этих ошибок tooresolve [tooupload AzureRmVhd добавить hello исходного VHD](https://msdn.microsoft.com/library/mt603554.aspx), доступны в локальной среде с hello одинаковое значение, что и hello ОС (обобщенный/специализированные).</span><span class="sxs-lookup"><span data-stu-id="7db4d-117">tooresolve both these errors, use [Add-AzureRmVhd tooupload hello original VHD](https://msdn.microsoft.com/library/mt603554.aspx), available on-premises, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="7db4d-118">tooupload как обобщены, сначала следует помнить toorun sysprep.</span><span class="sxs-lookup"><span data-stu-id="7db4d-118">tooupload as generalized, remember toorun sysprep first.</span></span>

<span data-ttu-id="7db4d-119">**Ошибки записи:**</span><span class="sxs-lookup"><span data-stu-id="7db4d-119">**Capture Errors:**</span></span>

<span data-ttu-id="7db4d-120">**N<sup>3</sup>:** Если hello ОС Windows обобщенный и записывается в виде специализированными, вы получите подготовки ошибка тайм-аута из-за hello исходной виртуальной Машины не может использоваться как она помечена как обобщенный.</span><span class="sxs-lookup"><span data-stu-id="7db4d-120">**N<sup>3</sup>:** If hello OS is Windows generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="7db4d-121">**N<sup>4</sup>:** Если специализированные Windows, и она записывается как обобщенный hello операционной системы, вы получите инициализации: сбой, так как hello новой виртуальной Машины, выполнив hello исходное имя компьютера, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="7db4d-121">**N<sup>4</sup>:** If hello OS is Windows specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username, and password.</span></span> <span data-ttu-id="7db4d-122">Кроме того, исходный hello виртуальной Машины не выполняется, так как она помечена как специальные.</span><span class="sxs-lookup"><span data-stu-id="7db4d-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="7db4d-123">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="7db4d-123">**Resolution**</span></span>

<span data-ttu-id="7db4d-124">tooresolve оба эти ошибки удалить текущее изображение hello из портала hello и [захватить снова из hello текущего виртуальные жесткие диски](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) с "hello" того же параметра, что и для hello ОС (обобщенный/специализированные).</span><span class="sxs-lookup"><span data-stu-id="7db4d-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a><span data-ttu-id="7db4d-125">Проблема: ошибка выделения (пользовательский образ, образ из коллекции или Marketplace)</span><span class="sxs-lookup"><span data-stu-id="7db4d-125">Issue: Custom/gallery/marketplace image; allocation failure</span></span>
<span data-ttu-id="7db4d-126">Эта ошибка возникает в ситуациях, при получении новой виртуальной Машины запроса hello закрепленных tooa кластера, либо не поддерживает размер виртуальной Машины hello запрашиваемого, либо не имеет доступного свободного места tooaccommodate hello запроса.</span><span class="sxs-lookup"><span data-stu-id="7db4d-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="7db4d-127">**Причина 1:** hello кластера не поддерживают hello запрошенный размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7db4d-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="7db4d-128">**Способ устранения 1.**</span><span class="sxs-lookup"><span data-stu-id="7db4d-128">**Resolution 1:**</span></span>

* <span data-ttu-id="7db4d-129">Повторите запрос hello, с использованием меньшего размера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7db4d-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="7db4d-130">Если hello запрошенный размер hello, что виртуальная машина нельзя изменить:</span><span class="sxs-lookup"><span data-stu-id="7db4d-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="7db4d-131">Остановите все виртуальные машины hello в наборе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="7db4d-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="7db4d-132">Для этого последовательно выберите **Группы ресурсов** > *имя вашей группы ресурсов* > **Ресурсы** > *имя вашей группы доступности* > **Виртуальные машины** > *имя вашей виртуальной машины* > **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="7db4d-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="7db4d-133">После всех hello остановка виртуальных машин, создайте hello новой виртуальной Машины в hello требуемого размера.</span><span class="sxs-lookup"><span data-stu-id="7db4d-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="7db4d-134">Запустить сначала hello новой виртуальной Машины, а затем выберите каждый hello остановлен, виртуальные машины и нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="7db4d-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="7db4d-135">**Причина 2:** hello кластер не имеет свободных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7db4d-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="7db4d-136">**Способ устранения 2.**</span><span class="sxs-lookup"><span data-stu-id="7db4d-136">**Resolution 2:**</span></span>

* <span data-ttu-id="7db4d-137">Повторите запрос hello позже.</span><span class="sxs-lookup"><span data-stu-id="7db4d-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="7db4d-138">Если hello новой виртуальной Машины можно указать различные доступности</span><span class="sxs-lookup"><span data-stu-id="7db4d-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="7db4d-139">Создание новой виртуальной Машины в наборе доступности на другой (в hello одного региона).</span><span class="sxs-lookup"><span data-stu-id="7db4d-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="7db4d-140">Добавление новой виртуальной Машины toohello hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7db4d-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7db4d-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7db4d-141">Next steps</span></span>
<span data-ttu-id="7db4d-142">При возникновении проблем во время запуска остановленной виртуальной машины Windows или в случае изменения размера существующей виртуальной машины Windows в Azure см. раздел [Устранение неполадок в развертывании Resource Manager при перезагрузке или изменении размера существующей виртуальной машины Windows в Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7db4d-142">If you encounter issues when you start a stopped Windows VM or resize an existing Windows VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

