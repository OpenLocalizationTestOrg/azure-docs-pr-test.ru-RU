---
title: "Настройка параметров репликации для Azure Site Recovery | Документация Майкрософт"
description: "В статье описано, как развернуть Site Recovery, чтобы управлять в Azure репликацией, отработкой отказа и восстановлением виртуальных машин Hyper-V, запущенных в облаках VMM."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 73a1f19177f23441f5f7165cf2bc92ba85e62aa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-replication-policy-for-vmware-to-azure"></a><span data-ttu-id="4a56d-103">Управление политикой репликации для VMware в Azure</span><span class="sxs-lookup"><span data-stu-id="4a56d-103">Manage replication policy for VMware to Azure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="4a56d-104">Создание политики репликации</span><span class="sxs-lookup"><span data-stu-id="4a56d-104">Create a replication policy</span></span>

1. <span data-ttu-id="4a56d-105">Выберите **Управление** > **Site Recovery Infrastructure** (Инфраструктура Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="4a56d-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="4a56d-106">В разделе **For VMware and Physical machines** (Для виртуальных машин VMware и физических компьютеров) выберите **Политики репликации**.</span><span class="sxs-lookup"><span data-stu-id="4a56d-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="4a56d-107">Щеклните **+Replication policy** (+ Политика репликации).</span><span class="sxs-lookup"><span data-stu-id="4a56d-107">Select **+Replication policy**.</span></span>

    ![Создание политики репликации](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="4a56d-109">Введите имя политики.</span><span class="sxs-lookup"><span data-stu-id="4a56d-109">Enter the policy name.</span></span>

5. <span data-ttu-id="4a56d-110">В поле **Пороговое значение RPO**укажите предельное значение целевой точки восстановления (RPO).</span><span class="sxs-lookup"><span data-stu-id="4a56d-110">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="4a56d-111">Если непрерывная репликация превышает это значение, выдаются оповещения.</span><span class="sxs-lookup"><span data-stu-id="4a56d-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="4a56d-112">В поле **Хранение точки восстановления** укажите период хранения каждой точки восстановления (в часах).</span><span class="sxs-lookup"><span data-stu-id="4a56d-112">In **Recovery point retention**, specify (in hours) the duration of the retention window for each recovery point.</span></span> <span data-ttu-id="4a56d-113">Защищенные компьютеры будут восстанавливаться до любой точки в пределах этого периода.</span><span class="sxs-lookup"><span data-stu-id="4a56d-113">Protected machines can be recovered to any point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4a56d-114">Для компьютеров, реплицируемых в хранилище уровня "Премиум", поддерживается хранение до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="4a56d-114">Up to 24 hours of retention is supported for machines replicated to premium storage.</span></span> <span data-ttu-id="4a56d-115">Для компьютеров, реплицируемых в хранилище уровня "Стандартный", поддерживается хранение до 72 часов.</span><span class="sxs-lookup"><span data-stu-id="4a56d-115">Up to 72 hours of retention is supported for machines replicated to standard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4a56d-116">Политика репликации для восстановления размещения создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="4a56d-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="4a56d-117">В поле **Периодичность создания моментальных снимков с согласованием приложений** укажите, с какой периодичностью (в минутах) будут создаваться точки восстановления, содержащие моментальные снимки, согласованные на уровне приложений.</span><span class="sxs-lookup"><span data-stu-id="4a56d-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="4a56d-118">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4a56d-118">Click **OK**.</span></span> <span data-ttu-id="4a56d-119">Политика будет создана в течение 30–60 секунд.</span><span class="sxs-lookup"><span data-stu-id="4a56d-119">The policy should be created in 30 to 60 seconds.</span></span>

![Создание политики репликации](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="4a56d-121">Связывание сервера конфигурации с политикой репликации</span><span class="sxs-lookup"><span data-stu-id="4a56d-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="4a56d-122">Щелкните политику репликации, с которой вы хотите связать сервер конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4a56d-122">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="4a56d-123">Щелкните **Связать**.</span><span class="sxs-lookup"><span data-stu-id="4a56d-123">Click **Associate**.</span></span>
<span data-ttu-id="4a56d-124">![Связывание сервера конфигурации](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="4a56d-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="4a56d-125">Выберите сервер конфигурации из списка серверов.</span><span class="sxs-lookup"><span data-stu-id="4a56d-125">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="4a56d-126">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4a56d-126">Click **OK**.</span></span> <span data-ttu-id="4a56d-127">Связь сервера конфигурации с политикой будет задана в течение 1–2 минут.</span><span class="sxs-lookup"><span data-stu-id="4a56d-127">The configuration server should be associated in one to two minutes.</span></span>

![Связывание сервера конфигурации](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="4a56d-129">Изменение политики репликации</span><span class="sxs-lookup"><span data-stu-id="4a56d-129">Edit a replication policy</span></span>
1. <span data-ttu-id="4a56d-130">Щелкните политику репликации, для которой вы хотите изменить параметры репликации.</span><span class="sxs-lookup"><span data-stu-id="4a56d-130">Choose the replication policy for which you want to edit replication settings.</span></span>
<span data-ttu-id="4a56d-131">![Изменение политики репликации](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="4a56d-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="4a56d-132">Нажмите **Изменить параметры**.</span><span class="sxs-lookup"><span data-stu-id="4a56d-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="4a56d-133">![Изменение параметров политики репликации](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="4a56d-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="4a56d-134">Измените параметры по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="4a56d-134">Change the settings based on your need.</span></span>
4. <span data-ttu-id="4a56d-135">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4a56d-135">Click **Save**.</span></span> <span data-ttu-id="4a56d-136">Политика будет сохранена в течение 2–5 минут в зависимости от количества виртуальных машин, использующих эту политику репликации.</span><span class="sxs-lookup"><span data-stu-id="4a56d-136">The policy should be saved in two to five minutes, depending on how many VMs are using that replication policy.</span></span>

![Сохранение политики репликации](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="4a56d-138">Отмена связи сервера конфигурации с политикой репликации</span><span class="sxs-lookup"><span data-stu-id="4a56d-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="4a56d-139">Щелкните политику репликации, с которой вы хотите связать сервер конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4a56d-139">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="4a56d-140">Щелкните **Отменить связь**.</span><span class="sxs-lookup"><span data-stu-id="4a56d-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="4a56d-141">Выберите сервер конфигурации из списка серверов.</span><span class="sxs-lookup"><span data-stu-id="4a56d-141">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="4a56d-142">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4a56d-142">Click **OK**.</span></span> <span data-ttu-id="4a56d-143">Связь сервера конфигурации с политикой будет отменена в течение 1–2 минут.</span><span class="sxs-lookup"><span data-stu-id="4a56d-143">The configuration server should be dissociated in one to two minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4a56d-144">Если хотя бы один реплицируемый элемент использует политику, то вы не сможете отменить ее связь с сервером конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4a56d-144">You cannot dissociate a configuration server if there is at least one replicated item using the policy.</span></span> <span data-ttu-id="4a56d-145">Прежде чем отменять связь политики с сервером, убедитесь, что ни один реплицируемый элемент не использует ее.</span><span class="sxs-lookup"><span data-stu-id="4a56d-145">Make sure there are no replicated items using the policy before you dissociate the configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="4a56d-146">Удаление политики репликации</span><span class="sxs-lookup"><span data-stu-id="4a56d-146">Delete a replication policy</span></span>

1. <span data-ttu-id="4a56d-147">Щелкните политику репликации, которую вы хотите удалить.</span><span class="sxs-lookup"><span data-stu-id="4a56d-147">Choose the replication policy that you want to delete.</span></span>
2. <span data-ttu-id="4a56d-148">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="4a56d-148">Click **Delete**.</span></span> <span data-ttu-id="4a56d-149">Политика будет удалена в течение 30–60 секунд.</span><span class="sxs-lookup"><span data-stu-id="4a56d-149">The policy should be deleted in 30 to 60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4a56d-150">Если с политикой репликации связан хотя бы один сервер конфигурации, вы не сможете удалить ее.</span><span class="sxs-lookup"><span data-stu-id="4a56d-150">You cannot delete a replication policy if it has at least one configuration server associated to it.</span></span> <span data-ttu-id="4a56d-151">Прежде чем удалять политику, убедитесь, что ни один реплицируемый элемент не использует ее, и удалите все связанные с ней серверы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4a56d-151">Make sure there are no replicated items using the policy and delete all the associated configuration servers before you delete the policy.</span></span>
