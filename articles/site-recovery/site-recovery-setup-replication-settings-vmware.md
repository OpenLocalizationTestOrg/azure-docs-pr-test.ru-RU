---
title: "aaaSet настроек репликации для Azure Site Recovery | Документы Microsoft"
description: "Описывает, каким образом облаков tooAzure toodeploy Site Recovery tooorchestrate репликации, отработки отказа и восстановления виртуальных машин Hyper-V в VMM."
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
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a><span data-ttu-id="513a4-103">Управление политикой репликации для VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="513a4-103">Manage replication policy for VMware tooAzure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="513a4-104">Создание политики репликации</span><span class="sxs-lookup"><span data-stu-id="513a4-104">Create a replication policy</span></span>

1. <span data-ttu-id="513a4-105">Выберите **Управление** > **Site Recovery Infrastructure** (Инфраструктура Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="513a4-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="513a4-106">В разделе **For VMware and Physical machines** (Для виртуальных машин VMware и физических компьютеров) выберите **Политики репликации**.</span><span class="sxs-lookup"><span data-stu-id="513a4-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="513a4-107">Щеклните **+Replication policy** (+ Политика репликации).</span><span class="sxs-lookup"><span data-stu-id="513a4-107">Select **+Replication policy**.</span></span>

    ![Создание политики репликации](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="513a4-109">Введите имя политики hello.</span><span class="sxs-lookup"><span data-stu-id="513a4-109">Enter hello policy name.</span></span>

5. <span data-ttu-id="513a4-110">В **пороговое значение RPO**, ограничить количество RPO hello.</span><span class="sxs-lookup"><span data-stu-id="513a4-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="513a4-111">Если непрерывная репликация превышает это значение, выдаются оповещения.</span><span class="sxs-lookup"><span data-stu-id="513a4-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="513a4-112">В **хранения точки восстановления**, укажите (в часах) hello продолжительность периода хранения hello для каждой точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="513a4-112">In **Recovery point retention**, specify (in hours) hello duration of hello retention window for each recovery point.</span></span> <span data-ttu-id="513a4-113">Защищенные виртуальные машины могут быть восстановлены tooany точка в пределах периода хранения.</span><span class="sxs-lookup"><span data-stu-id="513a4-113">Protected machines can be recovered tooany point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="513a4-114">Часы too24 удержания поддерживается для хранилища toopremium реплицированной машины.</span><span class="sxs-lookup"><span data-stu-id="513a4-114">Up too24 hours of retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="513a4-115">Часы too72 удержания поддерживается для хранилища toostandard реплицированной машины.</span><span class="sxs-lookup"><span data-stu-id="513a4-115">Up too72 hours of retention is supported for machines replicated toostandard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="513a4-116">Политика репликации для восстановления размещения создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="513a4-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="513a4-117">В поле **Периодичность создания моментальных снимков с согласованием приложений** укажите, с какой периодичностью (в минутах) будут создаваться точки восстановления, содержащие моментальные снимки, согласованные на уровне приложений.</span><span class="sxs-lookup"><span data-stu-id="513a4-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="513a4-118">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="513a4-118">Click **OK**.</span></span> <span data-ttu-id="513a4-119">Hello политики должны создаваться в течение 30 секунд too60.</span><span class="sxs-lookup"><span data-stu-id="513a4-119">hello policy should be created in 30 too60 seconds.</span></span>

![Создание политики репликации](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="513a4-121">Связывание сервера конфигурации с политикой репликации</span><span class="sxs-lookup"><span data-stu-id="513a4-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="513a4-122">Выберите политику toowhich hello репликации требуется tooassociate hello конфигурации сервера.</span><span class="sxs-lookup"><span data-stu-id="513a4-122">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="513a4-123">Щелкните **Связать**.</span><span class="sxs-lookup"><span data-stu-id="513a4-123">Click **Associate**.</span></span>
<span data-ttu-id="513a4-124">![Связывание сервера конфигурации](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="513a4-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="513a4-125">Выберите сервер конфигурации hello hello список серверов.</span><span class="sxs-lookup"><span data-stu-id="513a4-125">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="513a4-126">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="513a4-126">Click **OK**.</span></span> <span data-ttu-id="513a4-127">Сервер конфигурации Hello должен быть связан один tootwo минут.</span><span class="sxs-lookup"><span data-stu-id="513a4-127">hello configuration server should be associated in one tootwo minutes.</span></span>

![Связывание сервера конфигурации](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="513a4-129">Изменение политики репликации</span><span class="sxs-lookup"><span data-stu-id="513a4-129">Edit a replication policy</span></span>
1. <span data-ttu-id="513a4-130">Выберите политику репликации hello, для которого требуется tooedit настройки репликации.</span><span class="sxs-lookup"><span data-stu-id="513a4-130">Choose hello replication policy for which you want tooedit replication settings.</span></span>
<span data-ttu-id="513a4-131">![Изменение политики репликации](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="513a4-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="513a4-132">Нажмите **Изменить параметры**.</span><span class="sxs-lookup"><span data-stu-id="513a4-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="513a4-133">![Изменение параметров политики репликации](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="513a4-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="513a4-134">Измените параметры hello на основании потребностями.</span><span class="sxs-lookup"><span data-stu-id="513a4-134">Change hello settings based on your need.</span></span>
4. <span data-ttu-id="513a4-135">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="513a4-135">Click **Save**.</span></span> <span data-ttu-id="513a4-136">Hello политики должны сохраняться в течение двух минут toofive, в зависимости от того, сколько виртуальных машин с помощью этой политики репликации.</span><span class="sxs-lookup"><span data-stu-id="513a4-136">hello policy should be saved in two toofive minutes, depending on how many VMs are using that replication policy.</span></span>

![Сохранение политики репликации](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="513a4-138">Отмена связи сервера конфигурации с политикой репликации</span><span class="sxs-lookup"><span data-stu-id="513a4-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="513a4-139">Выберите политику toowhich hello репликации требуется tooassociate hello конфигурации сервера.</span><span class="sxs-lookup"><span data-stu-id="513a4-139">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="513a4-140">Щелкните **Отменить связь**.</span><span class="sxs-lookup"><span data-stu-id="513a4-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="513a4-141">Выберите сервер конфигурации hello hello список серверов.</span><span class="sxs-lookup"><span data-stu-id="513a4-141">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="513a4-142">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="513a4-142">Click **OK**.</span></span> <span data-ttu-id="513a4-143">Сервер конфигурации Hello следует несвязанной один tootwo минут.</span><span class="sxs-lookup"><span data-stu-id="513a4-143">hello configuration server should be dissociated in one tootwo minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="513a4-144">Невозможно разорвать связь сервера конфигурации, при наличии реплицированных хотя бы один элемент, с помощью политики hello.</span><span class="sxs-lookup"><span data-stu-id="513a4-144">You cannot dissociate a configuration server if there is at least one replicated item using hello policy.</span></span> <span data-ttu-id="513a4-145">Убедитесь, что нет реплицированных элементов с помощью политики hello, прежде чем отменить связь сервера конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="513a4-145">Make sure there are no replicated items using hello policy before you dissociate hello configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="513a4-146">Удаление политики репликации</span><span class="sxs-lookup"><span data-stu-id="513a4-146">Delete a replication policy</span></span>

1. <span data-ttu-id="513a4-147">Выберите политику репликации hello, которые должны toodelete.</span><span class="sxs-lookup"><span data-stu-id="513a4-147">Choose hello replication policy that you want toodelete.</span></span>
2. <span data-ttu-id="513a4-148">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="513a4-148">Click **Delete**.</span></span> <span data-ttu-id="513a4-149">следует удалить политики Hello too60 за 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="513a4-149">hello policy should be deleted in 30 too60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="513a4-150">Невозможно удалить политику репликации, если у него есть хотя бы один tooit конфигурации сервера, связанного.</span><span class="sxs-lookup"><span data-stu-id="513a4-150">You cannot delete a replication policy if it has at least one configuration server associated tooit.</span></span> <span data-ttu-id="513a4-151">Убедитесь, что нет реплицированных элементов с помощью политики hello и удалить все hello связанные серверы конфигурации, прежде чем удалять политику hello.</span><span class="sxs-lookup"><span data-stu-id="513a4-151">Make sure there are no replicated items using hello policy and delete all hello associated configuration servers before you delete hello policy.</span></span>
