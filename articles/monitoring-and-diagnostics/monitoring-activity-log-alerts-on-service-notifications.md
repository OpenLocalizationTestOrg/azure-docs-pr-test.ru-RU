---
title: "оповещения журнала действий aaaReceive службы уведомления о | Документы Microsoft"
description: "Получайте уведомления по SMS, электронной почте или от веб-перехватчика при использовании службы Azure."
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="1c3b6-103">Создание оповещений журнала действий для уведомлений службы</span><span class="sxs-lookup"><span data-stu-id="1c3b6-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="1c3b6-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="1c3b6-104">Overview</span></span>
<span data-ttu-id="1c3b6-105">В этой статье показано, как tooset копии журнала действий предупреждения для уведомления о работоспособности службы с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-105">This article shows you how tooset up activity log alerts for service health notifications by using hello Azure portal.</span></span>  

<span data-ttu-id="1c3b6-106">Может получать оповещение, когда Azure отправляет tooyour уведомления о работоспособности службы подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-106">You can receive an alert when Azure sends service health notifications tooyour Azure subscription.</span></span> <span data-ttu-id="1c3b6-107">Можно настроить предупреждения по hello:</span><span class="sxs-lookup"><span data-stu-id="1c3b6-107">You can configure hello alert based on:</span></span>

- <span data-ttu-id="1c3b6-108">Класс Hello уведомление о работоспособности службы (инцидент, обслуживания, сведения, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="1c3b6-108">hello class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="1c3b6-109">Затронутые службы Hello.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-109">hello service(s) affected.</span></span>
- <span data-ttu-id="1c3b6-110">Затронутые несоответствию Hello.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-110">hello region(s) affected.</span></span>
- <span data-ttu-id="1c3b6-111">состояние Hello hello уведомления (активных и разрешенных).</span><span class="sxs-lookup"><span data-stu-id="1c3b6-111">hello status of hello notification (active vs. resolved).</span></span>
- <span data-ttu-id="1c3b6-112">уровень Hello hello уведомления (информационные, предупреждения, ошибки).</span><span class="sxs-lookup"><span data-stu-id="1c3b6-112">hello level of hello notifications (informational, warning, error).</span></span>

<span data-ttu-id="1c3b6-113">Также можно настроить, должны отправляться предупреждение hello.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-113">You also can configure who hello alert should be sent to:</span></span>

- <span data-ttu-id="1c3b6-114">Выберите имеющуюся группу действий.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-114">Select an existing action group.</span></span>
- <span data-ttu-id="1c3b6-115">Создайте группу действий (которую можно будет использовать для будущих оповещений).</span><span class="sxs-lookup"><span data-stu-id="1c3b6-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="1c3b6-116">toolearn Дополнительные сведения о группах действия в разделе [создать действие групп и управление ими](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="1c3b6-116">toolearn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="1c3b6-117">Сведения о как уведомление о работоспособности службы tooconfigure предупреждений с помощью шаблонов диспетчера ресурсов Azure см. в разделе [шаблоны диспетчера ресурсов](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="1c3b6-117">For information on how tooconfigure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="1c3b6-118">Создать предупреждение на уведомление о работоспособности службы для новой группы действий с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="1c3b6-118">Create an alert on a service health notification for a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="1c3b6-119">В hello [портала](https://portal.azure.com)выберите **монитора**.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-119">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Hello «Монитор» службы](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="1c3b6-121">В hello **журнал действий** выберите **предупреждения**.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-121">In hello **Activity log** section, select **Alerts**.</span></span>

    ![Вкладка «Предупреждения» Hello](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="1c3b6-123">Выберите **журнала действий добавить оповещение**и заполните поля hello.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-123">Select **Add activity log alert**, and fill in hello fields.</span></span>

    ![Здравствуйте, команда «Добавить оповещение о активности журнала»](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="1c3b6-125">Введите имя в hello **имя предупреждения журнала действий** , введите в поле **описание**.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-125">Enter a name in hello **Activity log alert name** box, and provide a **Description**.</span></span>

    ![Hello «Добавить оповещение о журнала активности»-диалоговое окно](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="1c3b6-127">Hello **подписки** поле autofills с вашей текущей подписки.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-127">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="1c3b6-128">Эта подписка служит используется toosave hello активности журнала.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-128">This subscription is used toosave hello activity log alert.</span></span> <span data-ttu-id="1c3b6-129">ресурс предупреждения Hello — развернутой toothis подписки и мониторы событий в журнале активности hello для него.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-129">hello alert resource is deployed toothis subscription and monitors events in hello activity log for it.</span></span>

6. <span data-ttu-id="1c3b6-130">Выберите hello **группы ресурсов** в какой hello создается предупреждения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-130">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="1c3b6-131">Эта конфигурация не hello группы ресурсов, который отслеживается предупреждение hello.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-131">This isn't hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="1c3b6-132">Вместо этого он является hello группы ресурсов, где находится ресурс предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-132">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="1c3b6-133">В hello **категории событий** выберите **работоспособность службы**.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-133">In hello **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="1c3b6-134">При необходимости установите hello **службы**, **область**, **тип**, **состояние**, и **уровень** службы уведомления о работоспособности, которые должны tooreceive.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-134">Optionally, select hello **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want tooreceive.</span></span>

8. <span data-ttu-id="1c3b6-135">В разделе **предупреждения через**выберите hello **New** кнопка группы.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-135">Under **Alert via**, select hello **New** action group button.</span></span> <span data-ttu-id="1c3b6-136">Введите имя в hello **имя группы действий** поле и введите имя в hello **короткое имя** поле.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-136">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="1c3b6-137">Краткое имя Hello указывается в hello уведомлений, отправляемых при запуске этого оповещения.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-137">hello short name is referenced in hello notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="1c3b6-138">Определите список получателей, предоставляя hello получателя:</span><span class="sxs-lookup"><span data-stu-id="1c3b6-138">Define a list of receivers by providing hello receiver's:</span></span>

    <span data-ttu-id="1c3b6-139">а.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-139">a.</span></span> <span data-ttu-id="1c3b6-140">**Имя**: Введите имя получателя hello, псевдонима или идентификатор.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-140">**Name**: Enter hello receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="1c3b6-141">b.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-141">b.</span></span> <span data-ttu-id="1c3b6-142">**Тип действия.** Выберите SMS, электронную почту или веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="1c3b6-143">c.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-143">c.</span></span> <span data-ttu-id="1c3b6-144">**Сведения о**: в зависимости от выбранного типа действие hello, введите номер телефона, адрес электронной почты или веб-перехватчика URI.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-144">**Details**: Based on hello action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="1c3b6-145">Выберите **ОК** toocreate hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-145">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="1c3b6-146">В течение нескольких минут hello предупреждения является активным и начинает tootrigger на основе условий hello, указанное во время создания.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-146">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

<span data-ttu-id="1c3b6-147">Сведения о схеме веб-перехватчика hello для оповещения журнала действий см. в разделе [веб-перехватчиков для действия "Azure" журнал](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="1c3b6-147">For information on hello webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="1c3b6-148">Группа действий Hello, определенные в этом пошаговом руководстве для повторного использования для всех будущих определений предупреждений об изменении существующей группы действий.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-148">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="1c3b6-149">Создать предупреждение на уведомление о работоспособности службы для существующей группы действий с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="1c3b6-149">Create an alert on a service health notification for an existing action group by using hello Azure portal</span></span>

1. <span data-ttu-id="1c3b6-150">Выполните шаги 1 – 7 в предыдущем разделе toocreate hello уведомление о работоспособности вашей службы.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-150">Follow steps 1 through 7 in hello previous section toocreate your service health notification.</span></span> 

2. <span data-ttu-id="1c3b6-151">В разделе **предупреждения через**выберите hello **существующие** кнопка группы.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-151">Under **Alert via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="1c3b6-152">Выберите группу hello соответствующее действие.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-152">Select hello appropriate action group.</span></span>

3. <span data-ttu-id="1c3b6-153">Выберите **ОК** toocreate hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-153">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="1c3b6-154">В течение нескольких минут hello предупреждения является активным и начинает tootrigger на основе условий hello, указанное во время создания.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-154">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="1c3b6-155">Управление оповещениями</span><span class="sxs-lookup"><span data-stu-id="1c3b6-155">Manage your alerts</span></span>

<span data-ttu-id="1c3b6-156">После создания предупреждения, он отображается в hello **оповещения** раздел hello **монитор** колонку.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-156">After you create an alert, it's visible in hello **Alerts** section of hello **Monitor** blade.</span></span> <span data-ttu-id="1c3b6-157">Выберите оповещение hello toomanage для:</span><span class="sxs-lookup"><span data-stu-id="1c3b6-157">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="1c3b6-158">Изменить его.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-158">Edit it.</span></span>
* <span data-ttu-id="1c3b6-159">Удалить его.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-159">Delete it.</span></span>
* <span data-ttu-id="1c3b6-160">Включение и отключение, если требуется tootemporarily остановить или возобновить получать уведомления о предупреждении hello.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-160">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c3b6-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c3b6-161">Next steps</span></span>
- <span data-ttu-id="1c3b6-162">Дополнительные сведения об уведомлениях о работоспособности службы см. в [этой статье](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="1c3b6-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="1c3b6-163">Дополнительные сведения об ограничении частоты отправки уведомлений см. в статье [Ограничение частоты отправки для SMS, сообщений электронной почты и вызовов Webhook](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="1c3b6-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="1c3b6-164">Просмотрите hello [схема предупреждения веб-перехватчика журнала активности](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="1c3b6-164">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="1c3b6-165">Получить [Обзор оповещения журнала действий](monitoring-overview-alerts.md)и узнайте, как tooreceive предупреждения.</span><span class="sxs-lookup"><span data-stu-id="1c3b6-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span> 
- <span data-ttu-id="1c3b6-166">Дополнительные сведения о группах действий см. в статье [Создание групп действий и управление ими на портале Azure](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="1c3b6-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
