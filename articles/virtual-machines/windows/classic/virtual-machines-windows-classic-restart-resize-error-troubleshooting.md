---
title: "aaaVM перезапуске и изменении размера проблемы | Документы Microsoft"
description: "Устранение неполадок в классическом развертывании при перезагрузке или изменении размера существующей виртуальной машины Windows в Azure"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="09993-103">Устранение неполадок в классическом развертывании при перезагрузке или изменении размера существующей виртуальной машины Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="09993-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09993-104">Классический</span><span class="sxs-lookup"><span data-stu-id="09993-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="09993-105">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="09993-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="09993-106">При попытке toostart остановленной виртуальной машины (ВМ) Azure, или изменить размер существующей ВМ Azure, hello распространенных ошибок, возникающих — ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="09993-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="09993-107">Эта ошибка возникает, когда hello кластера или регион либо не имеет доступных ресурсов или не hello поддержки запрошенный размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="09993-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09993-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="09993-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="09993-109">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="09993-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="09993-110">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="09993-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="09993-111">Сбор журналов аудита</span><span class="sxs-lookup"><span data-stu-id="09993-111">Collect audit logs</span></span>
<span data-ttu-id="09993-112">Устранение неполадок, toostart hello сбора аудита записывает ошибку tooidentify hello, связанной с проблемой hello.</span><span class="sxs-lookup"><span data-stu-id="09993-112">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="09993-113">В hello портал Azure, щелкните **Обзор** > **виртуальные машины** > *виртуальной машины Windows*  >   **Параметры** > **журналы аудита**.</span><span class="sxs-lookup"><span data-stu-id="09993-113">In hello Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="09993-114">Проблема: ошибка во время запуска остановленной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="09993-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="09993-115">Повторите toostart остановленной виртуальной Машины, но получить ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="09993-115">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="09993-116">Причина:</span><span class="sxs-lookup"><span data-stu-id="09993-116">Cause</span></span>
<span data-ttu-id="09993-117">запрос Hello toostart hello остановлен, виртуальная машина имеет toobe попытки в hello исходного кластера, на котором размещена hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="09993-117">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="09993-118">Однако hello кластер не имеет запрос hello доступных toofulfill свободного места.</span><span class="sxs-lookup"><span data-stu-id="09993-118">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="09993-119">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="09993-119">Resolution</span></span>
* <span data-ttu-id="09993-120">Создайте новую облачную службу и свяжите ее с регионом или виртуальной сетью на основе региона, но не с территориальной группой.</span><span class="sxs-lookup"><span data-stu-id="09993-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="09993-121">Удалить hello остановлена виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="09993-121">Delete hello stopped VM.</span></span>
* <span data-ttu-id="09993-122">Повторно создайте hello виртуальной Машины в новой облачной службе hello с помощью дисков hello.</span><span class="sxs-lookup"><span data-stu-id="09993-122">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="09993-123">Запуск hello повторного создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="09993-123">Start hello re-created VM.</span></span>

<span data-ttu-id="09993-124">Если возникает сообщение об ошибке при попытке toocreate новой облачной службы, повторите попытку позже или изменить регион hello для hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="09993-124">If you get an error when trying toocreate a new cloud service, either retry later or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09993-125">Hello новой облачной службы будет новое имя и VIP, поэтому вам необходимо будет toochange эту информацию для всех зависимостей hello, которые используют эти сведения для hello существующей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="09993-125">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="09993-126">Проблема: ошибка при изменении размера существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="09993-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="09993-127">Повторите tooresize существующей виртуальной Машины, но получить ошибки выделения.</span><span class="sxs-lookup"><span data-stu-id="09993-127">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="09993-128">Причина:</span><span class="sxs-lookup"><span data-stu-id="09993-128">Cause</span></span>
<span data-ttu-id="09993-129">Hello hello tooresize виртуальная машина имеет toobe пытался выполнить запрос в исходном кластере hello, узлы hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="09993-129">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="09993-130">Однако кластер hello не поддерживает hello запрошенный размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="09993-130">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="09993-131">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="09993-131">Resolution</span></span>
<span data-ttu-id="09993-132">Уменьшить hello запрошенный размер виртуальной Машины и повторите hello изменения размера запроса.</span><span class="sxs-lookup"><span data-stu-id="09993-132">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="09993-133">Последовательно выберите **Просмотреть все** > **Виртуальные машины (классика)** > *имя своей виртуальной машины* > **Настройки** > **Размер**.</span><span class="sxs-lookup"><span data-stu-id="09993-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="09993-134">Подробные инструкции см. в разделе [изменить размер виртуальной машины hello](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="09993-134">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="09993-135">Если это не hello возможных tooreduce размер виртуальной Машины, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="09993-135">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="09993-136">Создать новую облачную службу, гарантируя, что он не связан tooan территориальную группу и не связан с виртуальной сети, связанные tooan территориальную группу.</span><span class="sxs-lookup"><span data-stu-id="09993-136">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="09993-137">Создайте в этой службе новую виртуальную машину большего размера.</span><span class="sxs-lookup"><span data-stu-id="09993-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="09993-138">Все виртуальные машины можно консолидировать в hello же облачной службе.</span><span class="sxs-lookup"><span data-stu-id="09993-138">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="09993-139">Если существующий облачная служба связана с виртуальной сети, основанный на области, можно соединить hello новой облачной службы toohello существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="09993-139">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="09993-140">Если hello существующей облачной службы не связан с виртуальной сетью, основанный на области, имеют toodelete hello виртуальных машин в существующей облачной службе hello затем повторно создать их в новой облачной службе hello из их дисков.</span><span class="sxs-lookup"><span data-stu-id="09993-140">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="09993-141">Однако это важно tooremember, что hello новой облачной службы будет новое имя и VIP, поэтому вам необходимо будет tooupdate эти данные для всех зависимостей hello, которые сейчас используют эту информацию для hello существующей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="09993-141">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09993-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09993-142">Next steps</span></span>
<span data-ttu-id="09993-143">При возникновении проблем во время создания виртуальной машины Windows в Azure ознакомьтесь со статьей, посвященной [устранению неполадок при развертывании](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="09993-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

