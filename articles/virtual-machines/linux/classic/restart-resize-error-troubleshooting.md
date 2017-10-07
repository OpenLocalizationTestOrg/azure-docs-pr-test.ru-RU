---
title: "aaaVM перезапуске и изменении размера проблемы | Документы Microsoft"
description: "Устранение неполадок в классическом развертывании при перезагрузке или изменении размера существующей виртуальной машины Linux в Azure."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: fb1dc88bb1b83043c434590118bc8810ad402872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="5835d-103">Устранение неполадок в классическом развертывании при перезагрузке или изменении размера существующей виртуальной машины Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="5835d-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5835d-104">Классический</span><span class="sxs-lookup"><span data-stu-id="5835d-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="5835d-105">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="5835d-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="5835d-106">При попытке toostart остановленной виртуальной машины (ВМ) Azure, или изменить размер существующей ВМ Azure, hello распространенных ошибок, возникающих — ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="5835d-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="5835d-107">Эта ошибка возникает, когда hello кластера или регион либо не имеет доступных ресурсов или не hello поддержки запрошенный размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5835d-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="5835d-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5835d-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5835d-109">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="5835d-109">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="5835d-110">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5835d-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="5835d-111">Hello диспетчера ресурсов версию в разделе [здесь](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5835d-111">For hello Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="5835d-112">Сбор журналов аудита</span><span class="sxs-lookup"><span data-stu-id="5835d-112">Collect audit logs</span></span>
<span data-ttu-id="5835d-113">Устранение неполадок, toostart hello сбора аудита записывает ошибку tooidentify hello, связанной с проблемой hello.</span><span class="sxs-lookup"><span data-stu-id="5835d-113">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="5835d-114">В hello портал Azure, щелкните **Обзор** > **виртуальные машины** > *к виртуальной машине Linux*  >   **Параметры** > **журналы аудита**.</span><span class="sxs-lookup"><span data-stu-id="5835d-114">In hello Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="5835d-115">Проблема: ошибка во время запуска остановленной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="5835d-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="5835d-116">Повторите toostart остановленной виртуальной Машины, но получить ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="5835d-116">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="5835d-117">Причина:</span><span class="sxs-lookup"><span data-stu-id="5835d-117">Cause</span></span>
<span data-ttu-id="5835d-118">запрос Hello toostart hello остановлен, виртуальная машина имеет toobe попытки в hello исходного кластера, на котором размещена hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5835d-118">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="5835d-119">Однако hello кластер не имеет запрос hello доступных toofulfill свободного места.</span><span class="sxs-lookup"><span data-stu-id="5835d-119">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="5835d-120">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="5835d-120">Resolution</span></span>
* <span data-ttu-id="5835d-121">Создайте новую облачную службу и свяжите ее с регионом или виртуальной сетью на основе региона, но не с территориальной группой.</span><span class="sxs-lookup"><span data-stu-id="5835d-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="5835d-122">Удалить hello остановлена виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5835d-122">Delete hello stopped VM.</span></span>
* <span data-ttu-id="5835d-123">Повторно создайте hello виртуальной Машины в новой облачной службе hello с помощью дисков hello.</span><span class="sxs-lookup"><span data-stu-id="5835d-123">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="5835d-124">Запуск hello повторного создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5835d-124">Start hello re-created VM.</span></span>

<span data-ttu-id="5835d-125">Если возникает сообщение об ошибке при попытке toocreate новой облачной службы, повторите попытку позднее или изменить регион hello для hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5835d-125">If you get an error when trying toocreate a new cloud service, either retry at a later time or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5835d-126">Hello новой облачной службы будет новое имя и VIP, поэтому вам необходимо будет toochange эту информацию для всех зависимостей hello, которые используют эти сведения для hello существующей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5835d-126">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="5835d-127">Проблема: ошибка при изменении размера существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="5835d-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="5835d-128">Повторите tooresize существующей виртуальной Машины, но получить ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="5835d-128">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="5835d-129">Причина:</span><span class="sxs-lookup"><span data-stu-id="5835d-129">Cause</span></span>
<span data-ttu-id="5835d-130">Hello hello tooresize виртуальная машина имеет toobe пытался выполнить запрос в исходном кластере hello, узлы hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5835d-130">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="5835d-131">Однако кластер hello не поддерживает hello запрошенный размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5835d-131">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="5835d-132">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="5835d-132">Resolution</span></span>
<span data-ttu-id="5835d-133">Уменьшить hello запрошенный размер виртуальной Машины и повторите hello изменения размера запроса.</span><span class="sxs-lookup"><span data-stu-id="5835d-133">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="5835d-134">Последовательно выберите **Просмотреть все** > **Виртуальные машины (классика)** > *имя своей виртуальной машины* > **Настройки** > **Размер**.</span><span class="sxs-lookup"><span data-stu-id="5835d-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="5835d-135">Подробные инструкции см. в разделе [изменить размер виртуальной машины hello](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="5835d-135">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="5835d-136">Если это не hello возможных tooreduce размер виртуальной Машины, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5835d-136">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="5835d-137">Создать новую облачную службу, гарантируя, что он не связан tooan территориальную группу и не связан с виртуальной сети, связанные tooan территориальную группу.</span><span class="sxs-lookup"><span data-stu-id="5835d-137">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="5835d-138">Создайте в этой службе новую виртуальную машину большего размера.</span><span class="sxs-lookup"><span data-stu-id="5835d-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="5835d-139">Все виртуальные машины можно консолидировать в hello же облачной службе.</span><span class="sxs-lookup"><span data-stu-id="5835d-139">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="5835d-140">Если существующий облачная служба связана с виртуальной сети, основанный на области, можно соединить hello новой облачной службы toohello существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="5835d-140">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="5835d-141">Если hello существующей облачной службы не связан с виртуальной сетью, основанный на области, имеют toodelete hello виртуальных машин в существующей облачной службе hello затем повторно создать их в новой облачной службе hello из их дисков.</span><span class="sxs-lookup"><span data-stu-id="5835d-141">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="5835d-142">Однако это важно tooremember, что hello новой облачной службы будет новое имя и VIP, поэтому вам необходимо будет tooupdate эти данные для всех зависимостей hello, которые сейчас используют эту информацию для hello существующей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5835d-142">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5835d-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5835d-143">Next steps</span></span>
<span data-ttu-id="5835d-144">При возникновении проблем во время создания виртуальной машины Linux в Azure см. статью, посвященную [устранению неполадок в развертывании](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5835d-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

