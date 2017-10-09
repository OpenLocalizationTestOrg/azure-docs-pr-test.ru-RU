---
title: "aaaCreate и управление группами действий в hello портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate групп действий в hello портал Azure и управление ими."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a><span data-ttu-id="46f4a-103">Создание и управление группами действий в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="46f4a-103">Create and manage action groups in hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="46f4a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="46f4a-104">Overview</span></span> ##
<span data-ttu-id="46f4a-105">В этой статье показано, как toocreate групп действий в hello портал Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="46f4a-105">This article shows you how toocreate and manage action groups in hello Azure portal.</span></span>

<span data-ttu-id="46f4a-106">Группы действий дают возможность настроить список действий.</span><span class="sxs-lookup"><span data-stu-id="46f4a-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="46f4a-107">Затем эти группы можно использовать при определении оповещений журнала действий.</span><span class="sxs-lookup"><span data-stu-id="46f4a-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="46f4a-108">Эти группы можно повторно использовать предупреждения журнала каждого действия, определяют, обеспечивая этой же действия выполняются каждый раз, когда оповещения hello активности журнала приветствия.</span><span class="sxs-lookup"><span data-stu-id="46f4a-108">These groups can then be reused by each activity log alert you define, ensuring that hello same actions are taken each time hello activity log alert is triggered.</span></span>

<span data-ttu-id="46f4a-109">Группа действий можно создать до too10 каждого типа действия.</span><span class="sxs-lookup"><span data-stu-id="46f4a-109">An action group can have up too10 of each action type.</span></span> <span data-ttu-id="46f4a-110">Каждое действие состоит из hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="46f4a-110">Each action is made up of hello following properties:</span></span>

* <span data-ttu-id="46f4a-111">**Имя**: Уникальный идентификатор в пределах группы действие hello.</span><span class="sxs-lookup"><span data-stu-id="46f4a-111">**Name**: A unique identifier within hello action group.</span></span>  
* <span data-ttu-id="46f4a-112">**Тип действия:** отправка SMS, электронного сообщения или вызов веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="46f4a-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="46f4a-113">**Сведения о**: hello соответствующий номер телефона, адрес электронной почты или веб-перехватчика URI.</span><span class="sxs-lookup"><span data-stu-id="46f4a-113">**Details**: hello corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="46f4a-114">Сведения о том, как группы действий tooconfigure шаблоны Azure Resource Manager toouse, в разделе [шаблоны диспетчера ресурсов группы действий](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="46f4a-114">For information on how toouse Azure Resource Manager templates tooconfigure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="46f4a-115">Создать группу действий с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="46f4a-115">Create an action group by using hello Azure portal</span></span> ##
1. <span data-ttu-id="46f4a-116">В hello [портала](https://portal.azure.com)выберите **монитора**.</span><span class="sxs-lookup"><span data-stu-id="46f4a-116">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="46f4a-117">Hello **монитор** колонке объединяет все мониторинга параметров и данных в одном представлении.</span><span class="sxs-lookup"><span data-stu-id="46f4a-117">hello **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Hello «Монитор» службы](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="46f4a-119">В hello **журнал действий** выберите **группы действий**.</span><span class="sxs-lookup"><span data-stu-id="46f4a-119">In hello **Activity log** section, select **Action groups**.</span></span>

    ![Вкладка «Группы действий» Hello](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="46f4a-121">Выберите **добавить действие группу**и заполните поля hello.</span><span class="sxs-lookup"><span data-stu-id="46f4a-121">Select **Add action group**, and fill in hello fields.</span></span>

    ![Здравствуйте, команда «Добавить группу действий»](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="46f4a-123">Введите имя в hello **имя группы действий** поле и введите имя в hello **короткое имя** поле.</span><span class="sxs-lookup"><span data-stu-id="46f4a-123">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="46f4a-124">Краткое имя Hello используется вместо действие полное имя группы, при отправке уведомлений с использованием этой группы.</span><span class="sxs-lookup"><span data-stu-id="46f4a-124">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![диалоговое окно Добавление действие Hello группы»](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="46f4a-126">Hello **подписки** поле autofills с вашей текущей подписки.</span><span class="sxs-lookup"><span data-stu-id="46f4a-126">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="46f4a-127">Эта подписка hello один находится в какой группе действие hello сохраняется.</span><span class="sxs-lookup"><span data-stu-id="46f4a-127">This subscription is hello one in which hello action group is saved.</span></span>

6. <span data-ttu-id="46f4a-128">Выберите hello **группы ресурсов** в действие, которое hello сохранить группу.</span><span class="sxs-lookup"><span data-stu-id="46f4a-128">Select hello **Resource group** in which hello action group is saved.</span></span>

7. <span data-ttu-id="46f4a-129">Определите список действий, указав для каждого из них следующие данные:</span><span class="sxs-lookup"><span data-stu-id="46f4a-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="46f4a-130">а.</span><span class="sxs-lookup"><span data-stu-id="46f4a-130">a.</span></span> <span data-ttu-id="46f4a-131">**Имя.** Введите уникальный идентификатор для этого действия.</span><span class="sxs-lookup"><span data-stu-id="46f4a-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="46f4a-132">b.</span><span class="sxs-lookup"><span data-stu-id="46f4a-132">b.</span></span> <span data-ttu-id="46f4a-133">**Тип действия.** Выберите SMS, электронную почту или веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="46f4a-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="46f4a-134">c.</span><span class="sxs-lookup"><span data-stu-id="46f4a-134">c.</span></span> <span data-ttu-id="46f4a-135">**Сведения о**: в зависимости от типа действия hello, введите номер телефона, адрес электронной почты или веб-перехватчика URI.</span><span class="sxs-lookup"><span data-stu-id="46f4a-135">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="46f4a-136">Выберите **ОК** группа действий toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="46f4a-136">Select **OK** toocreate hello action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="46f4a-137">Управление группами действий</span><span class="sxs-lookup"><span data-stu-id="46f4a-137">Manage your action groups</span></span> ##
<span data-ttu-id="46f4a-138">После создания группу действий, он отображается в hello **группы действий** раздел hello **монитор** колонку.</span><span class="sxs-lookup"><span data-stu-id="46f4a-138">After you create an action group, it's visible in hello **Action groups** section of hello **Monitor** blade.</span></span> <span data-ttu-id="46f4a-139">Выберите группу действие hello нужные toomanage для:</span><span class="sxs-lookup"><span data-stu-id="46f4a-139">Select hello action group you want toomanage to:</span></span>

* <span data-ttu-id="46f4a-140">добавлять, изменять или удалять действия;</span><span class="sxs-lookup"><span data-stu-id="46f4a-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="46f4a-141">Удалите группу действие hello.</span><span class="sxs-lookup"><span data-stu-id="46f4a-141">Delete hello action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46f4a-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="46f4a-142">Next steps</span></span> ##
* <span data-ttu-id="46f4a-143">Дополнительные сведения о поведении SMS-оповещений в группе действий см. в [этой статье](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="46f4a-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="46f4a-144">Получить [понимания схемы предупреждения веб-перехватчика журнала действие hello](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="46f4a-144">Gain an [understanding of hello activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="46f4a-145">Дополнительные сведения о лимитах для оповещений см. в статье [Ограничение частоты отправки для SMS, сообщений электронной почты и вызовов Webhook](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="46f4a-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="46f4a-146">Получить [Обзор оповещения журнала действий](monitoring-overview-alerts.md)и узнайте, как tooreceive предупреждения.</span><span class="sxs-lookup"><span data-stu-id="46f4a-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="46f4a-147">Узнайте, каким образом слишком[настроить оповещения при изменении отправленных уведомление о работоспособности службы](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="46f4a-147">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
