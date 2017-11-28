---
title: "Создание групп действий и управление ими на портале Azure | Документация Майкрософт"
description: "Узнайте, как создавать группы действий и управлять ими на портале Azure."
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
ms.openlocfilehash: ea15705bf02d9773507c6cb59f2da4c1dd0f9d77
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-action-groups-in-the-azure-portal"></a><span data-ttu-id="01532-103">Создание групп действий и управление ими на портале Azure</span><span class="sxs-lookup"><span data-stu-id="01532-103">Create and manage action groups in the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="01532-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="01532-104">Overview</span></span> ##
<span data-ttu-id="01532-105">В этой статье показано, как создавать группы действий и управлять ими на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="01532-105">This article shows you how to create and manage action groups in the Azure portal.</span></span>

<span data-ttu-id="01532-106">Группы действий дают возможность настроить список действий.</span><span class="sxs-lookup"><span data-stu-id="01532-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="01532-107">Затем эти группы можно использовать при определении оповещений журнала действий.</span><span class="sxs-lookup"><span data-stu-id="01532-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="01532-108">Эти группы можно повторно использовать в каждом определенном оповещении журнала действий, чтобы при появлении такого оповещения предпринимались одинаковые действия.</span><span class="sxs-lookup"><span data-stu-id="01532-108">These groups can then be reused by each activity log alert you define, ensuring that the same actions are taken each time the activity log alert is triggered.</span></span>

<span data-ttu-id="01532-109">Группа действий может содержать до 10 действий каждого типа.</span><span class="sxs-lookup"><span data-stu-id="01532-109">An action group can have up to 10 of each action type.</span></span> <span data-ttu-id="01532-110">Каждое действие состоит из следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="01532-110">Each action is made up of the following properties:</span></span>

* <span data-ttu-id="01532-111">**Имя:** уникальный идентификатор в группе действий.</span><span class="sxs-lookup"><span data-stu-id="01532-111">**Name**: A unique identifier within the action group.</span></span>  
* <span data-ttu-id="01532-112">**Тип действия:** отправка SMS, электронного сообщения или вызов веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="01532-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="01532-113">**Сведения:** соответствующий телефонный номер, адрес электронной почты или URI веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="01532-113">**Details**: The corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="01532-114">Дополнительные сведения о настройке групп действий с помощью шаблонов Azure Resource Manager см. в статье [Создание группы действий с помощью шаблона Resource Manager](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="01532-114">For information on how to use Azure Resource Manager templates to configure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-the-azure-portal"></a><span data-ttu-id="01532-115">Создание группы действий с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="01532-115">Create an action group by using the Azure portal</span></span> ##
1. <span data-ttu-id="01532-116">На [портале](https://portal.azure.com) выберите **Монитор**.</span><span class="sxs-lookup"><span data-stu-id="01532-116">In the [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="01532-117">В колонке **Монитор** объединены все параметры мониторинга и данные в одном представлении.</span><span class="sxs-lookup"><span data-stu-id="01532-117">The **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Служба "Монитор"](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="01532-119">В разделе **Журнал действий** выберите **Action groups** (Группы действий).</span><span class="sxs-lookup"><span data-stu-id="01532-119">In the **Activity log** section, select **Action groups**.</span></span>

    ![Вкладка Action groups (Группы действий)](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="01532-121">Выберите **Add action group** (Добавить группу действий) и заполните поля.</span><span class="sxs-lookup"><span data-stu-id="01532-121">Select **Add action group**, and fill in the fields.</span></span>

    ![Команда Add action group (Добавить группу действий)](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="01532-123">Введите имя в поля **Action group name** (Имя группы действий) и **Short name** (Короткое имя).</span><span class="sxs-lookup"><span data-stu-id="01532-123">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="01532-124">Короткое имя используется вместо полного имени группы действий при отправке уведомлений с помощью этой группы.</span><span class="sxs-lookup"><span data-stu-id="01532-124">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![Диалоговое окно Add action group (Добавить группу действий)](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="01532-126">Поле **Подписка** автоматически заполняется вашей текущей подпиской.</span><span class="sxs-lookup"><span data-stu-id="01532-126">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="01532-127">В этой подписке сохраняются группы действий.</span><span class="sxs-lookup"><span data-stu-id="01532-127">This subscription is the one in which the action group is saved.</span></span>

6. <span data-ttu-id="01532-128">Выберите **группу ресурсов**, в которой хранится группа действий.</span><span class="sxs-lookup"><span data-stu-id="01532-128">Select the **Resource group** in which the action group is saved.</span></span>

7. <span data-ttu-id="01532-129">Определите список действий, указав для каждого из них следующие данные:</span><span class="sxs-lookup"><span data-stu-id="01532-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="01532-130">а.</span><span class="sxs-lookup"><span data-stu-id="01532-130">a.</span></span> <span data-ttu-id="01532-131">**Имя.** Введите уникальный идентификатор для этого действия.</span><span class="sxs-lookup"><span data-stu-id="01532-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="01532-132">b.</span><span class="sxs-lookup"><span data-stu-id="01532-132">b.</span></span> <span data-ttu-id="01532-133">**Тип действия.** Выберите SMS, электронную почту или веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="01532-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="01532-134">c.</span><span class="sxs-lookup"><span data-stu-id="01532-134">c.</span></span> <span data-ttu-id="01532-135">**Подробные сведения.** В зависимости от выбранного типа действия укажите номер телефона, адрес электронной почты или универсальный код ресурса (URI) веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="01532-135">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="01532-136">Нажмите кнопку **ОК**, чтобы создать группу действий.</span><span class="sxs-lookup"><span data-stu-id="01532-136">Select **OK** to create the action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="01532-137">Управление группами действий</span><span class="sxs-lookup"><span data-stu-id="01532-137">Manage your action groups</span></span> ##
<span data-ttu-id="01532-138">Созданная группа действий будет отображаться в разделе **Action groups** (Группы действий) в колонке **Монитор**.</span><span class="sxs-lookup"><span data-stu-id="01532-138">After you create an action group, it's visible in the **Action groups** section of the **Monitor** blade.</span></span> <span data-ttu-id="01532-139">Выберите группу действий, которой необходимо управлять:</span><span class="sxs-lookup"><span data-stu-id="01532-139">Select the action group you want to manage to:</span></span>

* <span data-ttu-id="01532-140">добавлять, изменять или удалять действия;</span><span class="sxs-lookup"><span data-stu-id="01532-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="01532-141">удалить группу действий.</span><span class="sxs-lookup"><span data-stu-id="01532-141">Delete the action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01532-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01532-142">Next steps</span></span> ##
* <span data-ttu-id="01532-143">Дополнительные сведения о поведении SMS-оповещений в группе действий см. в [этой статье](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="01532-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="01532-144">Узнайте о [схеме веб-перехватчика для оповещений журнала действий](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="01532-144">Gain an [understanding of the activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="01532-145">Дополнительные сведения о лимитах для оповещений см. в статье [Ограничение частоты отправки для SMS, сообщений электронной почты и вызовов Webhook](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="01532-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="01532-146">Изучите [обзор оповещений журнала действий](monitoring-overview-alerts.md) и узнайте, как получать оповещения.</span><span class="sxs-lookup"><span data-stu-id="01532-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="01532-147">Узнайте, как [настроить оповещения при поступлении уведомлений о работоспособности службы](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="01532-147">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
