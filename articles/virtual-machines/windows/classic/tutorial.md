---
title: "aaaCreate виртуальной Машины в hello портал Azure | Документы Microsoft"
description: "Создание виртуальной машины Windows в hello портал Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a><span data-ttu-id="ef678-103">Создание виртуальной машины под управлением Windows в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ef678-103">Create a virtual machine running Windows in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef678-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ef678-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="ef678-105">PowerShell: классическое развертывание</span><span class="sxs-lookup"><span data-stu-id="ef678-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="ef678-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ef678-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ef678-107">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ef678-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ef678-108">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ef678-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ef678-109">Узнайте, каким образом слишком[выполните следующие действия, с помощью модели развертывания диспетчера ресурсов hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) с помощью hello **портал Azure**.</span><span class="sxs-lookup"><span data-stu-id="ef678-109">Learn how too[perform these steps using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using hello **Azure portal**.</span></span>

<span data-ttu-id="ef678-110">В этом учебнике показано как toocreate Azure виртуальной машины (VM) под управлением Windows в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ef678-110">This tutorial shows you how toocreate an Azure virtual machine (VM) running Windows in hello Azure portal.</span></span> <span data-ttu-id="ef678-111">Мы будем использовать образ Windows Server в качестве примера, но это только один из hello многие образы Azure предлагает.</span><span class="sxs-lookup"><span data-stu-id="ef678-111">We'll use a Windows Server image as an example, but that's just one of hello many images Azure offers.</span></span> <span data-ttu-id="ef678-112">Обратите внимание, что доступные образы зависят от подписки.</span><span class="sxs-lookup"><span data-stu-id="ef678-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="ef678-113">Например изображения рабочего стола Windows может быть доступен tooMSDN подписчиков.</span><span class="sxs-lookup"><span data-stu-id="ef678-113">For example, Windows desktop images may be available tooMSDN subscribers.</span></span>

<span data-ttu-id="ef678-114">В этом разделе показано, как toouse hello **мониторинга** в hello Azure tooselect портала и затем создать виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="ef678-114">This section shows you how toouse hello **Dashboard** in hello Azure portal tooselect and then create hello virtual machine.</span></span>

<span data-ttu-id="ef678-115">Можно также создавать виртуальные машины с помощью [собственных образов](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="ef678-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="ef678-116">toolearn об этом и других методов, в разделе [toocreate различными способами виртуальной машины Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef678-116">toolearn about this and other methods, see [Different ways toocreate a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <span data-ttu-id="ef678-117"><a id="createvirtualmachine"></a>Создание hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="ef678-117"><a id="createvirtualmachine"> </a>Create hello virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="ef678-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ef678-118">Next steps</span></span>
* <span data-ttu-id="ef678-119">Узнайте, каким образом слишком[создания виртуальной Машины с помощью модели развертывания диспетчера ресурсов hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ef678-119">Learn how too[create a VM using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure portal.</span></span>
* <span data-ttu-id="ef678-120">Войдите в систему виртуальной машины toohello.</span><span class="sxs-lookup"><span data-stu-id="ef678-120">Log on toohello virtual machine.</span></span> <span data-ttu-id="ef678-121">Инструкции см. в разделе [вход tooa виртуальной машины под управлением Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="ef678-121">For instructions, see [Log on tooa virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="ef678-122">Присоедините диск данных toostore.</span><span class="sxs-lookup"><span data-stu-id="ef678-122">Attach a disk toostore data.</span></span> <span data-ttu-id="ef678-123">Можно присоединять пустые диски и диски с данными.</span><span class="sxs-lookup"><span data-stu-id="ef678-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="ef678-124">Инструкции см. в разделе hello [присоединения данных диска tooa Windows виртуальную машину, созданную с помощью hello классической модели развертывания](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="ef678-124">For instructions, see hello [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](attach-disk.md).</span></span>
