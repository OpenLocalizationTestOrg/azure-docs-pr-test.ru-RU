---
title: "Неполадки при перезапуске или изменении размера виртуальной машины | Документация Майкрософт"
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
ms.openlocfilehash: 7fe0636366c60d4679cfc69bd96cd532695b080e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="2bc89-103">Устранение неполадок в классическом развертывании при перезагрузке или изменении размера существующей виртуальной машины Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="2bc89-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2bc89-104">Классический</span><span class="sxs-lookup"><span data-stu-id="2bc89-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="2bc89-105">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="2bc89-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="2bc89-106">Когда вы запускаете остановленную виртуальную машину Azure или изменяете размер существующей виртуальной машины Azure, часто возникает ошибка выделения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2bc89-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="2bc89-107">Это происходит, когда кластер или регион не имеют доступных ресурсов или не поддерживают запрашиваемый размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2bc89-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bc89-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2bc89-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="2bc89-109">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="2bc89-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="2bc89-110">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2bc89-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="2bc89-111">Сбор журналов аудита</span><span class="sxs-lookup"><span data-stu-id="2bc89-111">Collect audit logs</span></span>
<span data-ttu-id="2bc89-112">Для устранения неполадок прежде всего соберите журналы аудита, чтобы определить ошибку, связанную с этой проблемой.</span><span class="sxs-lookup"><span data-stu-id="2bc89-112">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="2bc89-113">На портале Azure последовательно выберите **Обзор** > **Виртуальные машины** > *имя вашей виртуальной машины Windows* > **Настройки** > **Журналы аудита**.</span><span class="sxs-lookup"><span data-stu-id="2bc89-113">In the Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="2bc89-114">Проблема: ошибка во время запуска остановленной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2bc89-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="2bc89-115">При попытке запустить остановленную виртуальную машину отображается сообщение об ошибке выделения.</span><span class="sxs-lookup"><span data-stu-id="2bc89-115">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="2bc89-116">Причина:</span><span class="sxs-lookup"><span data-stu-id="2bc89-116">Cause</span></span>
<span data-ttu-id="2bc89-117">Запрос на запуск остановленной виртуальной машины нужно выполнять в исходном кластере, в котором размещена облачная служба.</span><span class="sxs-lookup"><span data-stu-id="2bc89-117">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="2bc89-118">Но этот кластер не имеет свободного места для выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="2bc89-118">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="2bc89-119">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="2bc89-119">Resolution</span></span>
* <span data-ttu-id="2bc89-120">Создайте новую облачную службу и свяжите ее с регионом или виртуальной сетью на основе региона, но не с территориальной группой.</span><span class="sxs-lookup"><span data-stu-id="2bc89-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="2bc89-121">Удалите остановленную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="2bc89-121">Delete the stopped VM.</span></span>
* <span data-ttu-id="2bc89-122">Повторно создайте виртуальную машину в новой облачной службе с помощью дисков.</span><span class="sxs-lookup"><span data-stu-id="2bc89-122">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="2bc89-123">Запустите вновь созданную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="2bc89-123">Start the re-created VM.</span></span>

<span data-ttu-id="2bc89-124">Если при попытке создания облачной службы появляется сообщение об ошибке, повторите попытку позже или измените регион для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="2bc89-124">If you get an error when trying to create a new cloud service, either retry later or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bc89-125">Новая облачная служба будет иметь новое имя и новый виртуальный IP-адрес. Поэтому эти данные следует изменить для всех зависимостей, которые используют информацию о существующей облачной службе.</span><span class="sxs-lookup"><span data-stu-id="2bc89-125">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="2bc89-126">Проблема: ошибка при изменении размера существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2bc89-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="2bc89-127">При попытке изменить размер существующей виртуальной машины отображается сообщение об ошибке выделения.</span><span class="sxs-lookup"><span data-stu-id="2bc89-127">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="2bc89-128">Причина:</span><span class="sxs-lookup"><span data-stu-id="2bc89-128">Cause</span></span>
<span data-ttu-id="2bc89-129">Запрос на изменение размера виртуальной машины нужно выполнять в исходном кластере, в котором размещена облачная служба.</span><span class="sxs-lookup"><span data-stu-id="2bc89-129">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="2bc89-130">Но этот кластер не поддерживает запрашиваемый размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2bc89-130">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="2bc89-131">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="2bc89-131">Resolution</span></span>
<span data-ttu-id="2bc89-132">Уменьшите запрашиваемый размер виртуальной машины и повторите запрос на изменение размера.</span><span class="sxs-lookup"><span data-stu-id="2bc89-132">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="2bc89-133">Последовательно выберите **Просмотреть все** > **Виртуальные машины (классика)** > *имя своей виртуальной машины* > **Настройки** > **Размер**.</span><span class="sxs-lookup"><span data-stu-id="2bc89-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="2bc89-134">Подробные инструкции см. в статье [Перезапуск виртуальной машины](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="2bc89-134">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="2bc89-135">Если размер виртуальной машины уменьшить невозможно, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2bc89-135">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="2bc89-136">Создайте новую облачную службу, не связанную с территориальной группой или с виртуальной сетью, которая связана с территориальной группой.</span><span class="sxs-lookup"><span data-stu-id="2bc89-136">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="2bc89-137">Создайте в этой службе новую виртуальную машину большего размера.</span><span class="sxs-lookup"><span data-stu-id="2bc89-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="2bc89-138">Вы можете объединить все виртуальные машины в одной облачной службе.</span><span class="sxs-lookup"><span data-stu-id="2bc89-138">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="2bc89-139">Если существующая облачная служба связана с виртуальной сетью на основе региона, вы можете подключить новую облачную службу к существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="2bc89-139">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="2bc89-140">Если существующая облачная служба не связана с виртуальной сетью на основе региона, следует удалить виртуальные машины из существующей облачной службы и воссоздать их в новой облачной службе с помощью дисков.</span><span class="sxs-lookup"><span data-stu-id="2bc89-140">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="2bc89-141">Не забывайте, что новая облачная служба будет иметь новое имя и новый виртуальный IP-адрес. Следовательно, эти данные потребуется обновить для всех зависимостей, которые используют эту информацию о существующей облачной службе.</span><span class="sxs-lookup"><span data-stu-id="2bc89-141">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bc89-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2bc89-142">Next steps</span></span>
<span data-ttu-id="2bc89-143">При возникновении проблем во время создания виртуальной машины Windows в Azure ознакомьтесь со статьей, посвященной [устранению неполадок при развертывании](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2bc89-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

