---
title: "выдает aaaVM перезапуске и изменении размера в Azure | Документы Microsoft"
description: "Устранение неполадок в развертывании Resource Manager при перезагрузке или изменении размера существующей виртуальной машины Linux в Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="32bf9-103">Устранение неполадок в развертывании при перезагрузке или изменении размера существующей виртуальной машины Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="32bf9-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="32bf9-104">При попытке toostart остановленной виртуальной машины (ВМ) Azure, или изменить размер существующей ВМ Azure, hello распространенных ошибок, возникающих — ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="32bf9-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="32bf9-105">Эта ошибка возникает, когда hello кластера или регион либо не имеет доступных ресурсов или не hello поддержки запрошенный размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="32bf9-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="32bf9-106">Сбор журналов действий</span><span class="sxs-lookup"><span data-stu-id="32bf9-106">Collect activity logs</span></span>
<span data-ttu-id="32bf9-107">Устранение неполадок, toostart действие сбор hello записывает ошибку tooidentify hello, связанной с проблемой hello.</span><span class="sxs-lookup"><span data-stu-id="32bf9-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="32bf9-108">Hello следующие ссылки содержат подробные сведения о процессе hello:</span><span class="sxs-lookup"><span data-stu-id="32bf9-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="32bf9-109">Просмотр операций развертывания с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="32bf9-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="32bf9-110">Просматривать журналы действий toomanage Azure ресурсы</span><span class="sxs-lookup"><span data-stu-id="32bf9-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="32bf9-111">Проблема: ошибка во время запуска остановленной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="32bf9-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="32bf9-112">Повторите toostart остановленной виртуальной Машины, но получить ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="32bf9-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="32bf9-113">Причина:</span><span class="sxs-lookup"><span data-stu-id="32bf9-113">Cause</span></span>
<span data-ttu-id="32bf9-114">запрос Hello toostart hello остановлен, виртуальная машина имеет toobe попытки в hello исходного кластера, на котором размещена hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="32bf9-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="32bf9-115">Однако hello кластер не имеет запрос hello доступных toofulfill свободного места.</span><span class="sxs-lookup"><span data-stu-id="32bf9-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="32bf9-116">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="32bf9-116">Resolution</span></span>
* <span data-ttu-id="32bf9-117">Остановите все hello виртуальных машин в доступности hello установить, а затем перезапустите каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="32bf9-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="32bf9-118">Для этого последовательно выберите **Группы ресурсов** > *имя вашей группы ресурсов* > **Ресурсы** > *имя вашей группы доступности* > **Виртуальные машины** > *имя вашей виртуальной машины* > **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="32bf9-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="32bf9-119">После того как все Здравствуйте остановка виртуальных машин, выберите каждый hello остановлена виртуальные машины и нажмите кнопку Пуск.</span><span class="sxs-lookup"><span data-stu-id="32bf9-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="32bf9-120">Повторите запрос перезапуск hello позже.</span><span class="sxs-lookup"><span data-stu-id="32bf9-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="32bf9-121">Проблема: ошибка при изменении размера существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="32bf9-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="32bf9-122">Повторите tooresize существующей виртуальной Машины, но получить ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="32bf9-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="32bf9-123">Причина:</span><span class="sxs-lookup"><span data-stu-id="32bf9-123">Cause</span></span>
<span data-ttu-id="32bf9-124">Hello hello tooresize виртуальная машина имеет toobe пытался выполнить запрос в исходном кластере hello, узлы hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="32bf9-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="32bf9-125">Однако кластер hello не поддерживает hello запрошенный размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="32bf9-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="32bf9-126">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="32bf9-126">Resolution</span></span>
* <span data-ttu-id="32bf9-127">Повторите запрос hello, с использованием меньшего размера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="32bf9-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="32bf9-128">Если hello запрошенный размер hello, что виртуальная машина нельзя изменить:</span><span class="sxs-lookup"><span data-stu-id="32bf9-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="32bf9-129">Остановите все виртуальные машины hello в наборе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="32bf9-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="32bf9-130">Для этого последовательно выберите **Группы ресурсов** > *имя вашей группы ресурсов* > **Ресурсы** > *имя вашей группы доступности* > **Виртуальные машины** > *имя вашей виртуальной машины* > **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="32bf9-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="32bf9-131">После того как все Здравствуйте остановка виртуальных машин, изменение размера hello требуемого ВМ tooa большего размера.</span><span class="sxs-lookup"><span data-stu-id="32bf9-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="32bf9-132">Выберите hello размера виртуальной Машины и нажмите кнопку **запустить**, и затем запустите все hello остановлено виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="32bf9-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32bf9-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32bf9-133">Next steps</span></span>
<span data-ttu-id="32bf9-134">При возникновении проблем во время создания виртуальной машины Linux в Azure см. статью, посвященную [устранению неполадок в развертывании](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="32bf9-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

