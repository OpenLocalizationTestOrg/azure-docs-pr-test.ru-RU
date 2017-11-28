---
title: " Управление сервером обработки, запущенным в Azure (классическая модель) | Документация Майкрософт"
description: "В этой статье описывается, как настроить сервер отработки для восстановления размещения (классическая модель) в Azure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 479bbd207bcf715138c340f9e4d2634120bab85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="a5a29-103">Управление сервером обработки, запущенным в Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="a5a29-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a5a29-104">Классическая модель Azure</span><span class="sxs-lookup"><span data-stu-id="a5a29-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="a5a29-105">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="a5a29-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="a5a29-106">При наличии значительной задержки между виртуальной сетью Azure и локальной сетью при восстановлении размещения рекомендуется развертывать сервер обработки в Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a29-106">During failback, it is recommended to deploy Process Server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="a5a29-107">В этой статье описывается, как выполнить установку, настройку и администрирование серверов обработки, работающих в Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a29-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="a5a29-108">Эта статья предназначена для тех, кто использовал классическую модель развертывания для виртуальных машин при отработке отказа.</span><span class="sxs-lookup"><span data-stu-id="a5a29-108">This article is to be used if you used Classic as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="a5a29-109">Если вы использовали модель развертывания с помощью Resource Manager, выполните инструкции в разделе [Управление сервером обработки, запущенным в Azure (модель Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a5a29-109">If you used Resource Manager as the deployment model follow the steps in [How to set up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5a29-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a5a29-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="a5a29-111">Развертывание сервера обработки в Azure</span><span class="sxs-lookup"><span data-stu-id="a5a29-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="a5a29-112">В Azure Marketplace создайте виртуальную машину с помощью **Microsoft Azure Site Recovery Process Server V2**.</span><span class="sxs-lookup"><span data-stu-id="a5a29-112">In Azure Marketplace, create a virtual machine using the **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="a5a29-113">![](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)Marketplace_image_1</span><span class="sxs-lookup"><span data-stu-id="a5a29-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="a5a29-114">Выберите **классическую** модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="a5a29-114">Ensure that you select the deployment model as **Classic**</span></span> </br><span data-ttu-id="a5a29-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="a5a29-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="a5a29-116">В мастере создания виртуальной машины выберите "Основные параметры" и укажите подписку и расположение для отработки отказа виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a5a29-116">In the Create virtual machine wizard > Basic Settings, ensure you select the Subscription and Location to where you failed over the virtual machines.</span></span></br><span data-ttu-id="a5a29-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="a5a29-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="a5a29-118">Убедитесь, что виртуальная машина подключена к виртуальной сети Azure, к которой подключена виртуальная машина для отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="a5a29-118">Ensure that the virtual machine is connected to the Azure Virtual Network to which the failed over virtual machine is connected.</span></span></br><span data-ttu-id="a5a29-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="a5a29-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="a5a29-120">Подготовив виртуальную машину на сервере обработки, войдите и зарегистрируйтесь на сервере конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a5a29-120">Once the Process Server virtual machine is provisioned, you need to log in and register it with the Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="a5a29-121">Чтобы использовать этот сервер обработки для восстановления размещения, необходимо зарегистрировать его на локальном сервере конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a5a29-121">To be able to use this Process Server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="a5a29-122">Регистрация сервера обработки (запущенного в Azure) на сервере конфигурации (запущенного локально)</span><span class="sxs-lookup"><span data-stu-id="a5a29-122">Registering the Process Server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="a5a29-123">Обновление сервера обработки до последней версии</span><span class="sxs-lookup"><span data-stu-id="a5a29-123">Upgrading the Process Server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="a5a29-124">Отмена регистрации сервера обработки (запущенного в Azure) на сервере конфигурации (запущенного локально)</span><span class="sxs-lookup"><span data-stu-id="a5a29-124">Unregistering the Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
