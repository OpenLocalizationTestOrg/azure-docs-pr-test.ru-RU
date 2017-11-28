---
title: "aaaCreate виртуальную Машину с статический общедоступный IP-адрес - портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate ВМ с статических открытый IP адрес с помощью hello портал Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a><span data-ttu-id="ebbe9-103">Создайте виртуальную Машину с помощью hello портал Azure статический общедоступный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="ebbe9-103">Create a VM with a static public IP address using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ebbe9-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ebbe9-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="ebbe9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebbe9-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="ebbe9-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="ebbe9-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="ebbe9-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="ebbe9-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="ebbe9-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="ebbe9-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="ebbe9-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ebbe9-110">В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="ebbe9-111">Создание виртуальной машины со статическим общедоступным IP-адресом</span><span class="sxs-lookup"><span data-stu-id="ebbe9-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="ebbe9-112">toocreate виртуальную Машину с статический общедоступный IP-адрес адрес в hello портал Azure завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-112">toocreate a VM with a static public IP address in hello Azure portal, complete hello following steps:</span></span>

1. <span data-ttu-id="ebbe9-113">В браузере перейдите toohello [портал Azure](https://portal.azure.com) и, при необходимости, выполнить вход с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-113">From a browser, navigate toohello [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="ebbe9-114">Щелкните hello верхнем левом углу портала hello, **New**>>**вычислений**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-114">On hello top left hand corner of hello portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="ebbe9-115">В hello **выберите модель развертывания** выберите **диспетчера ресурсов** и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-115">In hello **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="ebbe9-116">В hello **основы** колонки, введите сведения о hello виртуальной Машины, как показано ниже и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-116">In hello **Basics** blade, enter hello VM information as shown below, and then click **OK**.</span></span>
   
    ![Портал Azure — основы](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="ebbe9-118">В hello **выберите размер** колонка, щелкните **A1 Standard** как показано ниже и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-118">In hello **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Портал Azure — выбор размера](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="ebbe9-120">В hello **параметры** колонка, щелкните **общедоступный IP-адрес**, затем в hello **создать общедоступный IP-адрес** колонки в разделе **назначения**, нажмите кнопку **Статических** как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-120">In hello **Settings** blade, click **Public IP address**, then in hello **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="ebbe9-121">Затем нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-121">And then click **OK**.</span></span>
   
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="ebbe9-123">В hello **параметры** колонка, щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-123">In hello **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="ebbe9-124">Просмотрите hello **Сводка** колонки, как показано ниже, а затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-124">Review hello **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="ebbe9-126">Обратите внимание, hello новую плитку на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-126">Notice hello new tile in your dashboard.</span></span>
   
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="ebbe9-128">После создания виртуальной Машины hello hello **параметры** колонке будет отображаться, как показано ниже</span><span class="sxs-lookup"><span data-stu-id="ebbe9-128">Once hello VM is created, hello **Settings** blade will be displayed as shown below</span></span>
    
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

