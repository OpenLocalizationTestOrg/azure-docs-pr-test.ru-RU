---
title: " Управление сервером обработки, запущенным в Azure (модель Resource Manager) | Документация Майкрософт"
description: "В этой статье описывает обработку tooset копирование и восстановление размещения сервера (диспетчер ресурсов) в Azure."
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
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="4c411-103">Управление сервером обработки, запущенным в Azure (модель Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="4c411-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c411-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="4c411-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="4c411-105">Классическая модель</span><span class="sxs-lookup"><span data-stu-id="4c411-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="4c411-106">При отработке отказа toodeploy сервера обработки в Azure рекомендуется при наличии высокой задержки между hello виртуальной сети Azure и локальной сетью.</span><span class="sxs-lookup"><span data-stu-id="4c411-106">During failback, it is recommended toodeploy process server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="4c411-107">В этой статье описывается, как установить, настроить и управлять серверами процесса hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="4c411-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="4c411-108">Эта статья является используется, если вы использовали toobe **диспетчера ресурсов** как hello модель развертывания для hello виртуальных машин во время отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="4c411-108">This article is toobe used if you used **Resource Manager** as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="4c411-109">Если вы использовали **классический** как hello модели развертывания, выполните действия hello в [как tooset о & Настройка восстановления размещения процесса сервера (классические)](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="4c411-109">If you used **Classic** as hello deployment model, follow hello steps in [How tooset up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c411-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4c411-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="4c411-111">Развертывание сервера обработки в Azure</span><span class="sxs-lookup"><span data-stu-id="4c411-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="4c411-112">В хранилище hello > **инфраструктура Site Recovery** (под заголовком «Manage» hello) > **серверы конфигурации** (под заголовком «Для VMware и физические компьютеры»), выберите сервер конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="4c411-112">In hello Vault > **Site Recovery Infrastructure** (under hello "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select hello configuration server.</span></span>
2. <span data-ttu-id="4c411-113">На приветствия сервера конфигурации сведения открывшейся странице нажмите кнопку «+ обработать сервера»</span><span class="sxs-lookup"><span data-stu-id="4c411-113">In hello Configuration Server details page that opens click "+ Process server"</span></span>

  ![Добавление коллекции сервера обработки](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="4c411-115">На hello **добавить сервер обработки** страницы выберите hello последующих значений</span><span class="sxs-lookup"><span data-stu-id="4c411-115">On hello **Add process server** page, select hello following values</span></span>

  ![Добавление элемента коллекции сервера обработки](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="4c411-117">**Имя поля**</span><span class="sxs-lookup"><span data-stu-id="4c411-117">**Field Name**</span></span>|<span data-ttu-id="4c411-118">**Значение**</span><span class="sxs-lookup"><span data-stu-id="4c411-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="4c411-119">Укажите, куда toodeploy сервера обработки</span><span class="sxs-lookup"><span data-stu-id="4c411-119">Choose where you want toodeploy your process server</span></span>|<span data-ttu-id="4c411-120">Выберите значение hello **развернуть сервер обработки восстановление после сбоя в Azure**</span><span class="sxs-lookup"><span data-stu-id="4c411-120">Select hello value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="4c411-121">Подписки</span><span class="sxs-lookup"><span data-stu-id="4c411-121">Subscription</span></span>|<span data-ttu-id="4c411-122">Выберите подписку Azure, где отработку отказа виртуальных машин hello hello</span><span class="sxs-lookup"><span data-stu-id="4c411-122">Select hello Azure Subscription where you failed over hello virtual machines</span></span>|
|<span data-ttu-id="4c411-123">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="4c411-123">Resource Group</span></span>|<span data-ttu-id="4c411-124">Можно создать toodeploy группы ресурсов этого процесса сервера или выберите сервер обработки toodeploy hello в существующую группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="4c411-124">You can create a Resource Group toodeploy this process server or choose toodeploy hello process server in an existing Resource Group</span></span>|
|<span data-ttu-id="4c411-125">Расположение</span><span class="sxs-lookup"><span data-stu-id="4c411-125">Location</span></span>|<span data-ttu-id="4c411-126">Выберите центр обработки данных Azure hello в виртуальных машин hello где отработку отказа в</span><span class="sxs-lookup"><span data-stu-id="4c411-126">Select hello Azure Data Center into which hello virtual machines where failed over into</span></span>|
|<span data-ttu-id="4c411-127">Сеть Azure</span><span class="sxs-lookup"><span data-stu-id="4c411-127">Azure Network</span></span>|<span data-ttu-id="4c411-128">Выберите hello Network(VNet) виртуального Azure, виртуальные машины hello где отработку отказа в.</span><span class="sxs-lookup"><span data-stu-id="4c411-128">Select hello Azure Virtual Network(VNet) that hello virtual machines where failed over into.</span></span> <span data-ttu-id="4c411-129">Если отработка отказа виртуальных машин выполняется в несколько виртуальных сетей Azure, сервер обработки нужно развернуть в каждую из них.</span><span class="sxs-lookup"><span data-stu-id="4c411-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="4c411-130">Заполните остальные hello hello свойства для сервера обработки hello</span><span class="sxs-lookup"><span data-stu-id="4c411-130">Fill in hello rest of hello properties for hello process server</span></span>

  ![Добавление сводных данных о сервере обработки](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="4c411-132">**Имя поля**</span><span class="sxs-lookup"><span data-stu-id="4c411-132">**Field Name**</span></span>|<span data-ttu-id="4c411-133">**Значение**</span><span class="sxs-lookup"><span data-stu-id="4c411-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="4c411-134">Имя сервера</span><span class="sxs-lookup"><span data-stu-id="4c411-134">Server Name</span></span>|<span data-ttu-id="4c411-135">Отображаемое имя и имя узла для виртуальной машины на сервере обработки.</span><span class="sxs-lookup"><span data-stu-id="4c411-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="4c411-136">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="4c411-136">User Name</span></span>|<span data-ttu-id="4c411-137">Имя пользователя, который становится администратором на этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4c411-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="4c411-138">Учетная запись хранения</span><span class="sxs-lookup"><span data-stu-id="4c411-138">Storage Account</span></span>|<span data-ttu-id="4c411-139">Имя учетной записи хранилища, там, где размещены виртуального диска виртуальной машины hello hello</span><span class="sxs-lookup"><span data-stu-id="4c411-139">Name of hello Storage Account where hello virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="4c411-140">Подсеть</span><span class="sxs-lookup"><span data-stu-id="4c411-140">Subnet</span></span>|<span data-ttu-id="4c411-141">подключен подсети Hello hello виртуальной сети Azure toowhich hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4c411-141">hello subnet of hello Azure VNet toowhich hello virtual machine is connected</span></span>|
| <span data-ttu-id="4c411-142">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="4c411-142">IP Address</span></span>|<span data-ttu-id="4c411-143">IP-адрес, желательно tooassume сервера hello процесса, когда он загружается</span><span class="sxs-lookup"><span data-stu-id="4c411-143">IP Address that you would like hello process server tooassume once it boots up</span></span>|
5. <span data-ttu-id="4c411-144">Щелкните toostart кнопку "ОК" hello, развертывание виртуальной машины hello процесса сервера.</span><span class="sxs-lookup"><span data-stu-id="4c411-144">Click hello OK button toostart deploying hello process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="4c411-145">возможности toouse toobe сервер обработки для восстановления размещения, должны tooregister его с сервера конфигурации локальной hello.</span><span class="sxs-lookup"><span data-stu-id="4c411-145">toobe able toouse this process server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="4c411-146">Регистрация hello процесса сервера (под управлением Azure) tooa конфигурации сервер (локальный)</span><span class="sxs-lookup"><span data-stu-id="4c411-146">Registering hello process server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="4c411-147">Обновление версии toolatest hello процесса сервера.</span><span class="sxs-lookup"><span data-stu-id="4c411-147">Upgrading hello process server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="4c411-148">Отмена регистрации hello процесса сервера (под управлением Azure) из конфигурации сервер (локальный)</span><span class="sxs-lookup"><span data-stu-id="4c411-148">Unregistering hello process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
