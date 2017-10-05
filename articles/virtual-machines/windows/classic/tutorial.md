---
title: "Создание виртуальной машины на портале Azure | Документация Майкрософт"
description: "Информация о создании виртуальной машины под управлением Windows на портале Azure."
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
ms.openlocfilehash: 0981872ff819fdf49a9cc97afce3c212013ce76b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-running-windows-in-the-azure-portal"></a><span data-ttu-id="97179-103">Создание виртуальной машины под управлением Windows на портале Azure</span><span class="sxs-lookup"><span data-stu-id="97179-103">Create a virtual machine running Windows in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97179-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="97179-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="97179-105">PowerShell: классическое развертывание</span><span class="sxs-lookup"><span data-stu-id="97179-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="97179-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="97179-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="97179-107">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="97179-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="97179-108">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="97179-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="97179-109">Узнайте, как [выполнить эти действия для модели развертывания с помощью Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), используя **портал Azure**.</span><span class="sxs-lookup"><span data-stu-id="97179-109">Learn how to [perform these steps using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using the **Azure portal**.</span></span>

<span data-ttu-id="97179-110">В этом руководстве показано, как создать виртуальную машину Azure под управлением Windows на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="97179-110">This tutorial shows you how to create an Azure virtual machine (VM) running Windows in the Azure portal.</span></span> <span data-ttu-id="97179-111">Мы будем использовать в качестве примера образ Windows Server, но это лишь один из многих образов, предлагаемых в Azure.</span><span class="sxs-lookup"><span data-stu-id="97179-111">We'll use a Windows Server image as an example, but that's just one of the many images Azure offers.</span></span> <span data-ttu-id="97179-112">Обратите внимание, что доступные образы зависят от подписки.</span><span class="sxs-lookup"><span data-stu-id="97179-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="97179-113">Например, подписчикам MSDN могут быть доступны образы рабочих столов Windows.</span><span class="sxs-lookup"><span data-stu-id="97179-113">For example, Windows desktop images may be available to MSDN subscribers.</span></span>

<span data-ttu-id="97179-114">В этом разделе рассматривается использование **панели мониторинга** на портале Azure для выбора и создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="97179-114">This section shows you how to use the **Dashboard** in the Azure portal to select and then create the virtual machine.</span></span>

<span data-ttu-id="97179-115">Можно также создавать виртуальные машины с помощью [собственных образов](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="97179-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="97179-116">Дополнительную информацию об этом и других методах см. в статье [Различные способы создания виртуальной машины Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97179-116">To learn about this and other methods, see [Different ways to create a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on the classic portal. -->

## <span data-ttu-id="97179-117"><a id="createvirtualmachine"> </a>Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="97179-117"><a id="createvirtualmachine"> </a>Create the virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="97179-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="97179-118">Next steps</span></span>
* <span data-ttu-id="97179-119">Узнайте, как [создать виртуальную машину для модели развертывания с помощью Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), используя портал Azure.</span><span class="sxs-lookup"><span data-stu-id="97179-119">Learn how to [create a VM using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in the Azure portal.</span></span>
* <span data-ttu-id="97179-120">Войдите в виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="97179-120">Log on to the virtual machine.</span></span> <span data-ttu-id="97179-121">Инструкции см. в статье [Вход в виртуальную машину под управлением Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="97179-121">For instructions, see [Log on to a virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="97179-122">Подключите диск для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="97179-122">Attach a disk to store data.</span></span> <span data-ttu-id="97179-123">Можно присоединять пустые диски и диски с данными.</span><span class="sxs-lookup"><span data-stu-id="97179-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="97179-124">Инструкции см. в статье [Подключение диска данных к виртуальной машине Windows, созданной с использованием классической модели развертывания](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="97179-124">For instructions, see the [Attach a data disk to a Windows virtual machine created with the classic deployment model](attach-disk.md).</span></span>
