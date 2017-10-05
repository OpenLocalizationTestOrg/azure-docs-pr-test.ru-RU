---
title: "Вход на классическую виртуальную машину Azure | Документация Майкрософт"
description: "Используйте портал Azure для входа в виртуальную машину Windows, созданную с использованием классической модели развертывания."
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
ms.openlocfilehash: 43d54de7e875de9212c23c49ad0539bf2272a312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="log-on-to-a-windows-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="0f27d-103">Вход в виртуальную машину под управлением Windows с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="0f27d-103">Log on to a Windows virtual machine using the Azure portal</span></span>
<span data-ttu-id="0f27d-104">На портале Azure для запуска сеанса удаленного рабочего стола и входа в виртуальную машину Windows используйте кнопку **Подключиться** .</span><span class="sxs-lookup"><span data-stu-id="0f27d-104">In the Azure portal, you use the **Connect** button to start a Remote Desktop session and log on to a Windows VM.</span></span>

<span data-ttu-id="0f27d-105">Хотите подключиться к виртуальной машине Linux?</span><span class="sxs-lookup"><span data-stu-id="0f27d-105">Do you want to connect to a Linux VM?</span></span> <span data-ttu-id="0f27d-106">Ознакомьтесь со статьей [How to log on to a virtual machine running Linux](../../linux/mac-create-ssh-keys.md) (Как войти в виртуальную машину под управлением Linux).</span><span class="sxs-lookup"><span data-stu-id="0f27d-106">See [How to log on to a virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how to [perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="0f27d-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0f27d-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0f27d-108">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="0f27d-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0f27d-109">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0f27d-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="0f27d-110">Дополнительные сведения о том, как войти в виртуальную машину с помощью модели Resource Manager, см. [здесь](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f27d-110">For information about how to log on to a VM using the Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="0f27d-111">Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="0f27d-111">Connect to the virtual machine</span></span>
1. <span data-ttu-id="0f27d-112">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0f27d-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="0f27d-113">Щелкните виртуальную машину, доступ к которой необходимо получить.</span><span class="sxs-lookup"><span data-stu-id="0f27d-113">Click on the virtual machine that you want to access.</span></span> <span data-ttu-id="0f27d-114">Имя указывается в области **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="0f27d-114">The name is listed in the **All resources** pane.</span></span>

    ![Расположения виртуальных машин](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="0f27d-116">Щелкните **Подключиться** на панели команд вверху панели мониторинга виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0f27d-116">Click **Connect** on the command bar atop the virtual machine dashboard.</span></span>

    ![Значок подключения для виртуальной машины](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If the **Connect** button isn't available, see the troubleshooting tips at the end of this article.
>
>
-->

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="0f27d-118">Вход на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="0f27d-118">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="0f27d-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f27d-119">Next steps</span></span>
* <span data-ttu-id="0f27d-120">Если кнопка **Подключиться** неактивна или возникли другие проблемы с подключением к удаленному рабочему столу, попробуйте переустановить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="0f27d-120">If the **Connect** button is inactive or you are having other problems with the Remote Desktop connection, try resetting the configuration.</span></span> <span data-ttu-id="0f27d-121">Щелкните **Сброс удаленного доступа** на панели мониторинга виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0f27d-121">click **Reset remote access** from the virtual machine dashboard.</span></span>

    ![Сброс удаленного доступа](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="0f27d-123">Если возникли проблемы с паролем, попробуйте сбросить его.</span><span class="sxs-lookup"><span data-stu-id="0f27d-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="0f27d-124">Щелкните **Сбросить пароль** возле левого края панели мониторинга виртуальной машины, в разделе **Поддержка и устранение неполадок**.</span><span class="sxs-lookup"><span data-stu-id="0f27d-124">Click **Reset password** along the left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Сброс пароля](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="0f27d-126">Если эти рекомендации не помогли устранить проблему или они вам не подходят, см. статью [Устранение неполадок с подключением к удаленному рабочему столу на виртуальной машине Azure под управлением Windows](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f27d-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="0f27d-127">В ней описывается процесс диагностики и решения распространенных проблем.</span><span class="sxs-lookup"><span data-stu-id="0f27d-127">This article walks you through diagnosing and resolving common problems.</span></span>
