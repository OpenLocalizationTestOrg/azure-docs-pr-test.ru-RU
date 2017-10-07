---
title: "выдает aaaVM перезапуске и изменении размера в Azure | Документы Microsoft"
description: "Устранение неполадок в развертывании Resource Manager при перезагрузке или изменении размера существующей виртуальной машины Windows в Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 0756b52d-4f5a-4503-ae45-c00a6a2edcdf
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.workload: required
ms.date: 06/13/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2cf7c2d19bf5f79fab4ffc0eff9ccc1182d601c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-windows-vm-in-azure"></a><span data-ttu-id="bd763-103">Устранение неполадок в развертывании при перезагрузке или изменении размера существующей виртуальной машины Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="bd763-103">Troubleshoot deployment issues with restarting or resizing an existing Windows VM in Azure</span></span>
<span data-ttu-id="bd763-104">При попытке toostart остановленной виртуальной машины (ВМ) Azure, или изменить размер существующей ВМ Azure, hello распространенных ошибок, возникающих — ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="bd763-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="bd763-105">Эта ошибка возникает, когда hello кластера или регион либо не имеет доступных ресурсов или не hello поддержки запрошенный размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bd763-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="bd763-106">Сбор журналов действий</span><span class="sxs-lookup"><span data-stu-id="bd763-106">Collect activity logs</span></span>
<span data-ttu-id="bd763-107">Устранение неполадок, toostart действие сбор hello записывает ошибку tooidentify hello, связанной с проблемой hello.</span><span class="sxs-lookup"><span data-stu-id="bd763-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="bd763-108">Hello следующие ссылки содержат подробные сведения о процессе hello:</span><span class="sxs-lookup"><span data-stu-id="bd763-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="bd763-109">Просмотр операций развертывания с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bd763-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="bd763-110">Просматривать журналы действий toomanage Azure ресурсы</span><span class="sxs-lookup"><span data-stu-id="bd763-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="bd763-111">Проблема: ошибка во время запуска остановленной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bd763-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="bd763-112">Повторите toostart остановленной виртуальной Машины, но получить ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="bd763-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="bd763-113">Причина:</span><span class="sxs-lookup"><span data-stu-id="bd763-113">Cause</span></span>
<span data-ttu-id="bd763-114">запрос Hello toostart hello остановлен, виртуальная машина имеет toobe попытки в hello исходного кластера, на котором размещена hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="bd763-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="bd763-115">Однако hello кластер не имеет запрос hello доступных toofulfill свободного места.</span><span class="sxs-lookup"><span data-stu-id="bd763-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="bd763-116">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="bd763-116">Resolution</span></span>
* <span data-ttu-id="bd763-117">Остановите все hello виртуальных машин в доступности hello установить, а затем перезапустите каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bd763-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="bd763-118">Для этого последовательно выберите **Группы ресурсов** > *имя вашей группы ресурсов* > **Ресурсы** > *имя вашей группы доступности* > **Виртуальные машины** > *имя вашей виртуальной машины* > **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="bd763-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="bd763-119">После того как все Здравствуйте остановка виртуальных машин, выберите каждый hello остановлена виртуальные машины и нажмите кнопку Пуск.</span><span class="sxs-lookup"><span data-stu-id="bd763-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="bd763-120">Повторите запрос перезапуск hello позже.</span><span class="sxs-lookup"><span data-stu-id="bd763-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="bd763-121">Проблема: ошибка при изменении размера существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bd763-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="bd763-122">Повторите tooresize существующей виртуальной Машины, но получить ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="bd763-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="bd763-123">Причина:</span><span class="sxs-lookup"><span data-stu-id="bd763-123">Cause</span></span>
<span data-ttu-id="bd763-124">Hello hello tooresize виртуальная машина имеет toobe пытался выполнить запрос в исходном кластере hello, узлы hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="bd763-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="bd763-125">Однако кластер hello не поддерживает hello запрошенный размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bd763-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="bd763-126">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="bd763-126">Resolution</span></span>
* <span data-ttu-id="bd763-127">Повторите запрос hello, с использованием меньшего размера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bd763-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="bd763-128">Если hello запрошенный размер hello, что виртуальная машина нельзя изменить:</span><span class="sxs-lookup"><span data-stu-id="bd763-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="bd763-129">Остановите все виртуальные машины hello в наборе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="bd763-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="bd763-130">Для этого последовательно выберите **Группы ресурсов** > *имя вашей группы ресурсов* > **Ресурсы** > *имя вашей группы доступности* > **Виртуальные машины** > *имя вашей виртуальной машины* > **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="bd763-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="bd763-131">После того как все Здравствуйте остановка виртуальных машин, изменение размера hello требуемого ВМ tooa большего размера.</span><span class="sxs-lookup"><span data-stu-id="bd763-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="bd763-132">Выберите hello размера виртуальной Машины и нажмите кнопку **запустить**, и затем запустите все hello остановлено виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="bd763-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd763-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bd763-133">Next steps</span></span>
<span data-ttu-id="bd763-134">При возникновении проблем во время создания виртуальной машины Windows в Azure ознакомьтесь со статьей, посвященной [устранению неполадок в развертывании](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd763-134">If you encounter issues when you create a new Windows VM in Azure, see [Troubleshoot deployment issues with creating a new Windows virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

