---
title: "Создание оповещений журнала действий | Документация Майкрософт"
description: "Уведомление посредством SMS, веб-перехватчика и электронной почты при возникновении определенных событий в журнале действий."
author: johnkemnetz
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: 3885469ec0e1fcc31386dd0ad7fe6cb5d03ab28e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="3597f-103">Создание оповещений журнала действий</span><span class="sxs-lookup"><span data-stu-id="3597f-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="3597f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="3597f-104">Overview</span></span>
<span data-ttu-id="3597f-105">Оповещения журнала действий создаются в тех случаях, когда происходит новое событие, записываемое в журнал действий, которое соответствует определенным условиям для оповещения.</span><span class="sxs-lookup"><span data-stu-id="3597f-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches the conditions specified in the alert.</span></span> <span data-ttu-id="3597f-106">Они являются ресурсами Azure, поэтому их можно создать с помощью шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3597f-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="3597f-107">Их также можно создать, обновить или удалить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3597f-107">They also can be created, updated, or deleted in the Azure portal.</span></span> <span data-ttu-id="3597f-108">В этой статье описаны принципы работы оповещений журнала действий.</span><span class="sxs-lookup"><span data-stu-id="3597f-108">This article introduces the concepts behind activity log alerts.</span></span> <span data-ttu-id="3597f-109">В ней также показано, как использовать портал Azure, чтобы настроить оповещения о событиях журнала действий.</span><span class="sxs-lookup"><span data-stu-id="3597f-109">It then shows you how to use the Azure portal to set up an alert on activity log events.</span></span>

<span data-ttu-id="3597f-110">Обычно оповещения журнала действий создаются для получения уведомлений в таких случаях:</span><span class="sxs-lookup"><span data-stu-id="3597f-110">Typically, you create activity log alerts to receive notifications when:</span></span>

* <span data-ttu-id="3597f-111">Внесение определенных изменений в ресурсы в вашей подписке Azure. Как правило, это конкретные группы ресурсов или ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3597f-111">Specific changes occur on resources in your Azure subscription, often scoped to particular resource groups or resources.</span></span> <span data-ttu-id="3597f-112">Например, можно получать уведомления при удалении любой виртуальной машины в группе ресурсов myProductionResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="3597f-112">For example, you might want to be notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="3597f-113">Или может потребоваться получать уведомления при назначении каких-либо новых ролей пользователю в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="3597f-113">Or, you might want to be notified if any new roles are assigned to a user in your subscription.</span></span>
* <span data-ttu-id="3597f-114">Возникновение события работоспособности службы.</span><span class="sxs-lookup"><span data-stu-id="3597f-114">A service health event occurs.</span></span> <span data-ttu-id="3597f-115">События работоспособности службы включают в себя уведомления об инцидентах и событиях обслуживания, относящихся к ресурсам в подписке.</span><span class="sxs-lookup"><span data-stu-id="3597f-115">Service health events include notification of incidents and maintenance events that apply to resources in your subscription.</span></span>

<span data-ttu-id="3597f-116">В любом случае оповещения журнала действий позволяют отслеживать только события в подписке, в которой создается оповещение.</span><span class="sxs-lookup"><span data-stu-id="3597f-116">In either case, an activity log alert monitors only for events in the subscription in which the alert is created.</span></span>

<span data-ttu-id="3597f-117">Оповещения журнала действий можно настроить на основе любого свойства верхнего уровня в объекте JSON для события журнала действий.</span><span class="sxs-lookup"><span data-stu-id="3597f-117">You can configure an activity log alert based on any top-level property in the JSON object for an activity log event.</span></span> <span data-ttu-id="3597f-118">Тем не менее на портале показаны наиболее распространенные варианты:</span><span class="sxs-lookup"><span data-stu-id="3597f-118">However, the portal shows the most common options:</span></span>

- <span data-ttu-id="3597f-119">**Категория.** Возможные значения: "Административный", "Работоспособность службы", "Автомасштабирование" или "Рекомендация".</span><span class="sxs-lookup"><span data-stu-id="3597f-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="3597f-120">Дополнительные сведения см. в разделе [Категории в журнале действий](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span><span class="sxs-lookup"><span data-stu-id="3597f-120">For more information, see [Overview of the Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="3597f-121">Дополнительные сведения о событиях службы работоспособности см. в статье [Создание оповещений журнала действий для уведомлений службы](./monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3597f-121">To learn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="3597f-122">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="3597f-122">**Resource group**</span></span>
- <span data-ttu-id="3597f-123">**Ресурс**</span><span class="sxs-lookup"><span data-stu-id="3597f-123">**Resource**</span></span>
- <span data-ttu-id="3597f-124">**Тип ресурса**</span><span class="sxs-lookup"><span data-stu-id="3597f-124">**Resource type**</span></span>
- <span data-ttu-id="3597f-125">**Имя операции.** Имя операции управления доступом на основе ролей диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3597f-125">**Operation name**: The Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="3597f-126">**Уровень.** Уровень серьезности события ("Подробный", "Информационное", "Предупреждение", "Ошибка" или "Критическое").</span><span class="sxs-lookup"><span data-stu-id="3597f-126">**Level**: The severity level of the event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="3597f-127">**Состояние.** Состояние события, обычно "Запущено", "Сбой" или "Успешно".</span><span class="sxs-lookup"><span data-stu-id="3597f-127">**Status**: The status of the event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="3597f-128">**Кем инициировано событие.** Это условие также называется "вызывающей стороной".</span><span class="sxs-lookup"><span data-stu-id="3597f-128">**Event initiated by**: Also known as the "caller."</span></span> <span data-ttu-id="3597f-129">Адрес электронной почты или идентификатор Azure Active Directory пользователя, выполнившего операцию.</span><span class="sxs-lookup"><span data-stu-id="3597f-129">The email address or Azure Active Directory identifier of the user who performed the operation.</span></span>

>[!NOTE]
><span data-ttu-id="3597f-130">В оповещении нужно указать по крайней мере два из указанных выше условий, одним из которых должна быть категория.</span><span class="sxs-lookup"><span data-stu-id="3597f-130">You must specify at least two of the preceding criteria in your alert, with one being the category.</span></span> <span data-ttu-id="3597f-131">Вы не можете создать оповещение, которое активируется каждый раз при создании события в журнале действий.</span><span class="sxs-lookup"><span data-stu-id="3597f-131">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
>
>

<span data-ttu-id="3597f-132">При активации оповещения журнала действий используется группа действий для создания действий или уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3597f-132">When an activity log alert is activated, it uses an action group to generate actions or notifications.</span></span> <span data-ttu-id="3597f-133">Группа действий — это многократно используемый набор приемников уведомлений, таких как адреса электронной почты, URL-адреса веб-перехватчиков или номера телефонов для отправки SMS.</span><span class="sxs-lookup"><span data-stu-id="3597f-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="3597f-134">На приемники можно ссылаться из нескольких уведомлений, чтобы централизовать и группировать каналы уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3597f-134">The receivers can be referenced from multiple alerts to centralize and group your notification channels.</span></span> <span data-ttu-id="3597f-135">Есть два способа определения оповещения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="3597f-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="3597f-136">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="3597f-136">You can:</span></span>

* <span data-ttu-id="3597f-137">Использовать имеющуюся группу действий в оповещении журнала действий.</span><span class="sxs-lookup"><span data-stu-id="3597f-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="3597f-138">Создать группу действий.</span><span class="sxs-lookup"><span data-stu-id="3597f-138">Create a new action group.</span></span> 

<span data-ttu-id="3597f-139">Дополнительные сведения о группах действия см. в статье [Создание групп действий и управление ими на портале Azure](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="3597f-139">To learn more about action groups, see [Create and manage action groups in the Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="3597f-140">Дополнительные сведения об уведомлениях о работоспособности службы см. в статье [Создание оповещений журнала действий для уведомлений службы](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3597f-140">To learn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="3597f-141">Создание оповещения для событий журнала действий с новой группой действий с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="3597f-141">Create an alert on an activity log event with a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="3597f-142">На [портале](https://portal.azure.com) выберите **Монитор**.</span><span class="sxs-lookup"><span data-stu-id="3597f-142">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Служба "Монитор"](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="3597f-144">В разделе **Журнал действий** выберите **Оповещения**.</span><span class="sxs-lookup"><span data-stu-id="3597f-144">In the **Activity log** section, select **Alerts**.</span></span>

    ![Вкладка "Оповещения"](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="3597f-146">Выберите **Add activity log alert** (Добавить оповещение журнала действий) и заполните поля.</span><span class="sxs-lookup"><span data-stu-id="3597f-146">Select **Add activity log alert**, and fill in the fields.</span></span>

4. <span data-ttu-id="3597f-147">Введите имя в поле **Activity log alert name** (Имя оповещения журнала действий), а затем выберите **Описание**.</span><span class="sxs-lookup"><span data-stu-id="3597f-147">Enter a name in the **Activity log alert name** box, and select a **Description**.</span></span>

    ![Команда Add activity log alert (Добавить оповещение журнала действий)](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="3597f-149">Поле **Подписка** автоматически заполняется вашей текущей подпиской.</span><span class="sxs-lookup"><span data-stu-id="3597f-149">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="3597f-150">В этой подписке сохраняются группы действий.</span><span class="sxs-lookup"><span data-stu-id="3597f-150">This subscription is the one in which the action group is saved.</span></span> <span data-ttu-id="3597f-151">Кроме того, в ней будет развернут ресурс оповещения и будут отслеживаться события журнала действий.</span><span class="sxs-lookup"><span data-stu-id="3597f-151">The alert resource is deployed to this subscription and monitors activity log events from it.</span></span>

    ![Диалоговое окно Add activity log alert (Добавить оповещение журнала действий)](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="3597f-153">Выберите **группу ресурсов**, в которой создается ресурс оповещения.</span><span class="sxs-lookup"><span data-stu-id="3597f-153">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="3597f-154">Эта группа ресурсов не отслеживается в оповещении.</span><span class="sxs-lookup"><span data-stu-id="3597f-154">This is not the resource group that's monitored by the alert.</span></span> <span data-ttu-id="3597f-155">В ней расположен ресурс оповещения.</span><span class="sxs-lookup"><span data-stu-id="3597f-155">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="3597f-156">При необходимости выберите **Категория событий**, чтобы изменить отобразившиеся дополнительные фильтры.</span><span class="sxs-lookup"><span data-stu-id="3597f-156">Optionally, select an **Event category** to modify the additional filters that are shown.</span></span> <span data-ttu-id="3597f-157">Для административных событий есть такие фильтры, как **Группа ресурсов**, **Ресурс**, **Тип ресурса**, **Имя операции**, **Уровень**, **Состояние** и **Event initiated by** (Кем инициировано событие).</span><span class="sxs-lookup"><span data-stu-id="3597f-157">For Administrative events, the filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="3597f-158">Эти значения определяют, какие события должны отслеживать это предупреждение.</span><span class="sxs-lookup"><span data-stu-id="3597f-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3597f-159">В оповещении необходимо указать хотя бы одно из описанных выше условий.</span><span class="sxs-lookup"><span data-stu-id="3597f-159">You must specify at least one of the preceding criteria in your alert.</span></span> <span data-ttu-id="3597f-160">Вы не можете создать оповещение, которое активируется каждый раз при создании события в журнале действий.</span><span class="sxs-lookup"><span data-stu-id="3597f-160">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
    >
    >

8. <span data-ttu-id="3597f-161">Введите имя в поля **Action group name** (Имя группы действий) и **Short name** (Короткое имя).</span><span class="sxs-lookup"><span data-stu-id="3597f-161">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="3597f-162">Короткое имя используется вместо полного имени группы действий при отправке уведомлений с помощью этой группы.</span><span class="sxs-lookup"><span data-stu-id="3597f-162">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="3597f-163">Определите список действий, указав для каждого из них следующие данные:</span><span class="sxs-lookup"><span data-stu-id="3597f-163">Define a list of actions by providing the action’s:</span></span>

    <span data-ttu-id="3597f-164">а.</span><span class="sxs-lookup"><span data-stu-id="3597f-164">a.</span></span> <span data-ttu-id="3597f-165">**Имя.** Введите имя, псевдоним или идентификатор действия.</span><span class="sxs-lookup"><span data-stu-id="3597f-165">**Name**: Enter the action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="3597f-166">b.</span><span class="sxs-lookup"><span data-stu-id="3597f-166">b.</span></span> <span data-ttu-id="3597f-167">**Тип действия.** Выберите SMS, электронную почту или веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="3597f-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="3597f-168">c.</span><span class="sxs-lookup"><span data-stu-id="3597f-168">c.</span></span> <span data-ttu-id="3597f-169">**Подробные сведения.** В зависимости от выбранного типа действия укажите номер телефона, адрес электронной почты или универсальный код ресурса (URI) веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="3597f-169">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="3597f-170">Нажмите кнопку **ОК**, чтобы создать оповещение.</span><span class="sxs-lookup"><span data-stu-id="3597f-170">Select **OK** to create the alert.</span></span>

<span data-ttu-id="3597f-171">Может потребоваться несколько минут на полное распространение оповещения, после чего оно становится активным.</span><span class="sxs-lookup"><span data-stu-id="3597f-171">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="3597f-172">Оповещение активируется, когда новые события соответствуют его условиям.</span><span class="sxs-lookup"><span data-stu-id="3597f-172">It triggers when new events match the alert's criteria.</span></span>

<span data-ttu-id="3597f-173">Дополнительные сведения см. в статье [Объекты webhook для оповещений журнала действий Azure](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="3597f-173">For more information, see [Understand the webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="3597f-174">Группу действий, определенную при выполнении этих шагов, можно использовать повторно в качестве имеющейся группы действий для всех будущих определений оповещений.</span><span class="sxs-lookup"><span data-stu-id="3597f-174">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="3597f-175">Создание оповещения для событий журнала действий для имеющейся группы действий с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="3597f-175">Create an alert on an activity log event for an existing action group by using the Azure portal</span></span>
1. <span data-ttu-id="3597f-176">Выполните шаги 1–7 в предыдущем разделе для создания оповещения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="3597f-176">Follow steps 1 through 7 in the previous section to create your activity log alert.</span></span>

2. <span data-ttu-id="3597f-177">В разделе **Notify via** (Уведомить по) нажмите кнопку группы действий **Существующий**.</span><span class="sxs-lookup"><span data-stu-id="3597f-177">Under **Notify via**, select the **Existing** action group button.</span></span> <span data-ttu-id="3597f-178">Выберите имеющуюся группу действий из списка.</span><span class="sxs-lookup"><span data-stu-id="3597f-178">Select an existing action group from the list.</span></span>

3. <span data-ttu-id="3597f-179">Нажмите кнопку **ОК**, чтобы создать оповещение.</span><span class="sxs-lookup"><span data-stu-id="3597f-179">Select **OK** to create the alert.</span></span>

<span data-ttu-id="3597f-180">Может потребоваться несколько минут на полное распространение оповещения, после чего оно становится активным.</span><span class="sxs-lookup"><span data-stu-id="3597f-180">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="3597f-181">Оповещение активируется, когда новые события соответствуют его условиям.</span><span class="sxs-lookup"><span data-stu-id="3597f-181">It triggers when new events match the alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="3597f-182">Управление оповещениями</span><span class="sxs-lookup"><span data-stu-id="3597f-182">Manage your alerts</span></span>

<span data-ttu-id="3597f-183">Созданное оповещение отображается в разделе "Оповещения" в колонке "Монитор".</span><span class="sxs-lookup"><span data-stu-id="3597f-183">After you create an alert, it's visible in the Alerts section of the Monitor blade.</span></span> <span data-ttu-id="3597f-184">Выберите оповещение, которым нужно управлять, чтобы получить возможность:</span><span class="sxs-lookup"><span data-stu-id="3597f-184">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="3597f-185">Изменить его.</span><span class="sxs-lookup"><span data-stu-id="3597f-185">Edit it.</span></span>
* <span data-ttu-id="3597f-186">Удалить его.</span><span class="sxs-lookup"><span data-stu-id="3597f-186">Delete it.</span></span>
* <span data-ttu-id="3597f-187">Отключить и включить его, если нужно временно остановить или возобновить получение уведомлений для этого оповещения.</span><span class="sxs-lookup"><span data-stu-id="3597f-187">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3597f-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3597f-188">Next steps</span></span>
- <span data-ttu-id="3597f-189">Ознакомьтесь с [обзором оповещений](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="3597f-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="3597f-190">Дополнительные сведения об ограничении частоты отправки уведомлений см. в статье [Ограничение частоты отправки для SMS, сообщений электронной почты и вызовов Webhook](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="3597f-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="3597f-191">Просмотрите схему веб-перехватчика оповещений журнала действий в статье [Объекты webhook для оповещений журнала действий Azure](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="3597f-191">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="3597f-192">Дополнительные сведения о группах действий см. в статье [Создание групп действий и управление ими на портале Azure](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="3597f-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="3597f-193">Дополнительные сведения об уведомлениях о работоспособности службы см. в [этой статье](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3597f-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="3597f-194">Создайте [оповещение журнала действий, чтобы отслеживать все операции системы автомасштабирования в своей подписке](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="3597f-194">Create an [activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="3597f-195">Создайте [оповещение журнала действий, чтобы отслеживать все ошибки автомасштабирования в своей подписке](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="3597f-195">Create an [activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
