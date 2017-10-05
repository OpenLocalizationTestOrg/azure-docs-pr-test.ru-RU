---
title: "Создание виртуальной машины со статическим общедоступным IP-адресом с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как создать виртуальную машину со статическим общедоступным IP-адресом с помощью портала Azure."
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
ms.openlocfilehash: 233e4eea8439320c1c7446e2c2b2e9d379351a3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-portal"></a><span data-ttu-id="8bf2c-103">Создание виртуальной машины со статическим общедоступным IP-адресом с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="8bf2c-103">Create a VM with a static public IP address using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8bf2c-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="8bf2c-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="8bf2c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bf2c-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="8bf2c-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8bf2c-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="8bf2c-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="8bf2c-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="8bf2c-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="8bf2c-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="8bf2c-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8bf2c-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8bf2c-110">В этой статье описывается использование модели развертывания c помощью Resource Manager. Для большинства новых развертываний мы рекомендуем использовать эту модель вместо классической.</span><span class="sxs-lookup"><span data-stu-id="8bf2c-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="8bf2c-111">Создание виртуальной машины со статическим общедоступным IP-адресом</span><span class="sxs-lookup"><span data-stu-id="8bf2c-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="8bf2c-112">Чтобы создать виртуальную машину со статическим общедоступным IP-адресом на портале Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="8bf2c-112">To create a VM with a static public IP address in the Azure portal, complete the following steps:</span></span>

1. <span data-ttu-id="8bf2c-113">В браузере откройте [портал Azure](https://portal.azure.com) и при необходимости войдите с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="8bf2c-113">From a browser, navigate to the [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="8bf2c-114">В верхнем левом углу портала щелкните **Создать**>>**Вычисления**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="8bf2c-114">On the top left hand corner of the portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="8bf2c-115">В списке **Выбор модели развертывания** выберите **Resource Manager** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8bf2c-115">In the **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="8bf2c-116">В колонке **Основы** введите сведения о виртуальной машине, как показано ниже, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8bf2c-116">In the **Basics** blade, enter the VM information as shown below, and then click **OK**.</span></span>
   
    ![Портал Azure — основы](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="8bf2c-118">В колонке **Выбор размера** щелкните **A1 Standard**, как показано ниже, и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8bf2c-118">In the **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Портал Azure — выбор размера](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="8bf2c-120">В колонке **Параметры** щелкните **Общедоступный IP-адрес**, а затем в колонке **Создать общедоступный IP-адрес** в разделе **Назначения** выберите **Статический**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8bf2c-120">In the **Settings** blade, click **Public IP address**, then in the **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="8bf2c-121">Затем нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8bf2c-121">And then click **OK**.</span></span>
   
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="8bf2c-123">В колонке **Параметры** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8bf2c-123">In the **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="8bf2c-124">Просмотрите колонку **Сводка**, как показано ниже, а затем нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8bf2c-124">Review the **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="8bf2c-126">Обратите внимание на новую плитку на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8bf2c-126">Notice the new tile in your dashboard.</span></span>
   
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="8bf2c-128">После создания виртуальной машины колонка **Параметры** будет отображаться, как показано ниже</span><span class="sxs-lookup"><span data-stu-id="8bf2c-128">Once the VM is created, the **Settings** blade will be displayed as shown below</span></span>
    
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

