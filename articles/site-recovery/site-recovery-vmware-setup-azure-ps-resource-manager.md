---
title: " Управление сервером обработки, запущенным в Azure (модель Resource Manager) | Документация Майкрософт"
description: "В этой статье описывается, как настроить сервер отработки для восстановления размещения (модель Resource Manager) в Azure."
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
ms.openlocfilehash: 2b9b31abd5d11d02935a74e47d26be9803cdc920
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="752fe-103">Управление сервером обработки, запущенным в Azure (модель Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="752fe-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="752fe-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="752fe-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="752fe-105">Классическая модель</span><span class="sxs-lookup"><span data-stu-id="752fe-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="752fe-106">При наличии значительной задержки между виртуальной сетью Azure и локальной сетью при восстановлении размещения рекомендуется развертывать сервер обработки в Azure.</span><span class="sxs-lookup"><span data-stu-id="752fe-106">During failback, it is recommended to deploy process server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="752fe-107">В этой статье описывается, как выполнить установку, настройку и администрирование серверов обработки, работающих в Azure.</span><span class="sxs-lookup"><span data-stu-id="752fe-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="752fe-108">В статье описано, как использовать **Resource Manager** как модель развертывания для виртуальных машин при отработке отказа.</span><span class="sxs-lookup"><span data-stu-id="752fe-108">This article is to be used if you used **Resource Manager** as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="752fe-109">Если вы используете **классическую** модель развертывания, выполните действия по [установке и настройке сервера обработки для восстановления размещения (классическая модель)](./site-recovery-vmware-setup-azure-ps-classic.md).</span><span class="sxs-lookup"><span data-stu-id="752fe-109">If you used **Classic** as the deployment model, follow the steps in [How to set up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="752fe-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="752fe-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="752fe-111">Развертывание сервера обработки в Azure</span><span class="sxs-lookup"><span data-stu-id="752fe-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="752fe-112">В хранилище выберите **Инфраструктура Site Recovery** (под заголовком "Управление") > **Серверы конфигурации** (под заголовком "Для VMware и физических компьютеров") и укажите сервер конфигурации.</span><span class="sxs-lookup"><span data-stu-id="752fe-112">In the Vault > **Site Recovery Infrastructure** (under the "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select the configuration server.</span></span>
2. <span data-ttu-id="752fe-113">На открывшейся странице со сведениями о конфигурации сервера нажмите кнопку "+Сервер обработки".</span><span class="sxs-lookup"><span data-stu-id="752fe-113">In the Configuration Server details page that opens click "+ Process server"</span></span>

  ![Добавление коллекции сервера обработки](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="752fe-115">На странице **Добавление сервера обработки** выберите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="752fe-115">On the **Add process server** page, select the following values</span></span>

  ![Добавление элемента коллекции сервера обработки](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="752fe-117">**Имя поля**</span><span class="sxs-lookup"><span data-stu-id="752fe-117">**Field Name**</span></span>|<span data-ttu-id="752fe-118">**Значение**</span><span class="sxs-lookup"><span data-stu-id="752fe-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="752fe-119">Выберите расположение для развертывания сервера обработки.</span><span class="sxs-lookup"><span data-stu-id="752fe-119">Choose where you want to deploy your process server</span></span>|<span data-ttu-id="752fe-120">Выберите вариант с **развертыванием сервера обработки для восстановления размещения в Azure**.</span><span class="sxs-lookup"><span data-stu-id="752fe-120">Select the value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="752fe-121">Подписки</span><span class="sxs-lookup"><span data-stu-id="752fe-121">Subscription</span></span>|<span data-ttu-id="752fe-122">Выберите подписку Azure для отработки отказа виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="752fe-122">Select the Azure Subscription where you failed over the virtual machines</span></span>|
|<span data-ttu-id="752fe-123">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="752fe-123">Resource Group</span></span>|<span data-ttu-id="752fe-124">Вы можете создать группу ресурсов для развертывания этого сервера обработки или развернуть сервер обработки в существующую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="752fe-124">You can create a Resource Group to deploy this process server or choose to deploy the process server in an existing Resource Group</span></span>|
|<span data-ttu-id="752fe-125">Расположение</span><span class="sxs-lookup"><span data-stu-id="752fe-125">Location</span></span>|<span data-ttu-id="752fe-126">Выберите центр обработки данных Azure для отработки отказа виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="752fe-126">Select the Azure Data Center into which the virtual machines where failed over into</span></span>|
|<span data-ttu-id="752fe-127">Сеть Azure</span><span class="sxs-lookup"><span data-stu-id="752fe-127">Azure Network</span></span>|<span data-ttu-id="752fe-128">Выберите виртуальную сеть Azure (VNet) для отработки отказа виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="752fe-128">Select the Azure Virtual Network(VNet) that the virtual machines where failed over into.</span></span> <span data-ttu-id="752fe-129">Если отработка отказа виртуальных машин выполняется в несколько виртуальных сетей Azure, сервер обработки нужно развернуть в каждую из них.</span><span class="sxs-lookup"><span data-stu-id="752fe-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="752fe-130">Укажите остальные свойства для сервера обработки.</span><span class="sxs-lookup"><span data-stu-id="752fe-130">Fill in the rest of the properties for the process server</span></span>

  ![Добавление сводных данных о сервере обработки](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="752fe-132">**Имя поля**</span><span class="sxs-lookup"><span data-stu-id="752fe-132">**Field Name**</span></span>|<span data-ttu-id="752fe-133">**Значение**</span><span class="sxs-lookup"><span data-stu-id="752fe-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="752fe-134">Имя сервера</span><span class="sxs-lookup"><span data-stu-id="752fe-134">Server Name</span></span>|<span data-ttu-id="752fe-135">Отображаемое имя и имя узла для виртуальной машины на сервере обработки.</span><span class="sxs-lookup"><span data-stu-id="752fe-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="752fe-136">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="752fe-136">User Name</span></span>|<span data-ttu-id="752fe-137">Имя пользователя, который становится администратором на этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="752fe-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="752fe-138">Учетная запись хранения</span><span class="sxs-lookup"><span data-stu-id="752fe-138">Storage Account</span></span>|<span data-ttu-id="752fe-139">Имя учетной записи хранения, где размещен виртуальный диск виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="752fe-139">Name of the Storage Account where the virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="752fe-140">Подсеть</span><span class="sxs-lookup"><span data-stu-id="752fe-140">Subnet</span></span>|<span data-ttu-id="752fe-141">Подсеть виртуальной сети Azure, к которой подключена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="752fe-141">The subnet of the Azure VNet to which the virtual machine is connected</span></span>|
| <span data-ttu-id="752fe-142">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="752fe-142">IP Address</span></span>|<span data-ttu-id="752fe-143">IP-адрес, используемый сервером обработки после загрузки.</span><span class="sxs-lookup"><span data-stu-id="752fe-143">IP Address that you would like the process server to assume once it boots up</span></span>|
5. <span data-ttu-id="752fe-144">Нажмите кнопку "ОК", чтобы начать развертывание виртуальной машины на сервере обработки.</span><span class="sxs-lookup"><span data-stu-id="752fe-144">Click the OK button to start deploying the process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="752fe-145">Чтобы использовать этот сервер обработки для восстановления размещения, необходимо зарегистрировать его на локальном сервере конфигурации.</span><span class="sxs-lookup"><span data-stu-id="752fe-145">To be able to use this process server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="752fe-146">Регистрация сервера обработки (запущенного в Azure) на сервере конфигурации (запущенного локально)</span><span class="sxs-lookup"><span data-stu-id="752fe-146">Registering the process server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="752fe-147">Обновление сервера обработки до последней версии</span><span class="sxs-lookup"><span data-stu-id="752fe-147">Upgrading the process server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="752fe-148">Отмена регистрации сервера обработки (запущенного в Azure) на сервере конфигурации (запущенного локально)</span><span class="sxs-lookup"><span data-stu-id="752fe-148">Unregistering the process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
