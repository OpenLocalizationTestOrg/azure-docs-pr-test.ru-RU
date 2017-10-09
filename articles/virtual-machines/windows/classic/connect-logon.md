---
title: "aaaLog на tooa классической виртуальной Машине Azure | Документы Microsoft"
description: "Используйте hello Azure портала toolog на виртуальной машине Windows tooa, созданных с помощью hello классической модели развертывания."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="e714c-103">Войдите на tooa виртуальной машины Windows с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="e714c-103">Log on tooa Windows virtual machine using hello Azure portal</span></span>
<span data-ttu-id="e714c-104">Hello портал Azure, используется в hello **Connect** кнопку toostart сеанс удаленного рабочего стола и войдите в систему виртуальной Машины Windows tooa.</span><span class="sxs-lookup"><span data-stu-id="e714c-104">In hello Azure portal, you use hello **Connect** button toostart a Remote Desktop session and log on tooa Windows VM.</span></span>

<span data-ttu-id="e714c-105">Вы хотите, чтобы tooconnect tooa виртуальных Машин Linux?</span><span class="sxs-lookup"><span data-stu-id="e714c-105">Do you want tooconnect tooa Linux VM?</span></span> <span data-ttu-id="e714c-106">В разделе [как toolog на tooa виртуальной машине под управлением Linux](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="e714c-106">See [How toolog on tooa virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="e714c-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e714c-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e714c-108">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="e714c-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e714c-109">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e714c-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e714c-110">Сведения о как toolog на tooa виртуальной Машины с помощью hello диспетчера ресурсов модели см. в разделе [здесь](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e714c-110">For information about how toolog on tooa VM using hello Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="e714c-111">Подключение toohello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e714c-111">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="e714c-112">Войдите в систему toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e714c-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="e714c-113">Щелкните на виртуальной машине hello, tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e714c-113">Click on hello virtual machine that you want tooaccess.</span></span> <span data-ttu-id="e714c-114">Hello имя указано в hello **все ресурсы** области.</span><span class="sxs-lookup"><span data-stu-id="e714c-114">hello name is listed in hello **All resources** pane.</span></span>

    ![Расположения виртуальных машин](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="e714c-116">Нажмите кнопку **Connect** на панели команд hello поверх панели мониторинга виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="e714c-116">Click **Connect** on hello command bar atop hello virtual machine dashboard.</span></span>

    ![Значок для виртуальной машины hello подключения](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="e714c-118">Войдите на виртуальную машину toohello</span><span class="sxs-lookup"><span data-stu-id="e714c-118">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="e714c-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e714c-119">Next steps</span></span>
* <span data-ttu-id="e714c-120">Если hello **Connect** кнопка неактивна, или возникли другие проблемы с подключением удаленного рабочего стола hello, попробуйте сбросить настройки hello.</span><span class="sxs-lookup"><span data-stu-id="e714c-120">If hello **Connect** button is inactive or you are having other problems with hello Remote Desktop connection, try resetting hello configuration.</span></span> <span data-ttu-id="e714c-121">Нажмите кнопку **сбросьте удаленный доступ** из панели мониторинга виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="e714c-121">click **Reset remote access** from hello virtual machine dashboard.</span></span>

    ![Сброс удаленного доступа](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="e714c-123">Если возникли проблемы с паролем, попробуйте сбросить его.</span><span class="sxs-lookup"><span data-stu-id="e714c-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="e714c-124">Нажмите кнопку **сброс пароля** вдоль hello левого края панели мониторинга виртуальной машины, в разделе **поддержки + Устранение неполадок**.</span><span class="sxs-lookup"><span data-stu-id="e714c-124">Click **Reset password** along hello left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Сброс пароля](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="e714c-126">Если эти советы не работают или не то, что нужно, в разделе [tooa подключений удаленного рабочего стола на устранение неполадок виртуальной машины на основе Windows Azure](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e714c-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e714c-127">В ней описывается процесс диагностики и решения распространенных проблем.</span><span class="sxs-lookup"><span data-stu-id="e714c-127">This article walks you through diagnosing and resolving common problems.</span></span>
