---
title: "оповещения aaaCreate для служб Azure - портал Azure | Документы Microsoft"
description: "Триггер сообщения электронной почты, уведомления, вызовите URL-адреса веб-сайтов (веб-перехватчиков) или автоматизации при соблюдении заданных условий hello."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="ec8fb-103">Создание оповещений метрик в Azure Monitor для служб Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="ec8fb-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec8fb-104">Портал</span><span class="sxs-lookup"><span data-stu-id="ec8fb-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="ec8fb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec8fb-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="ec8fb-106">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="ec8fb-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="ec8fb-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="ec8fb-107">Overview</span></span>
<span data-ttu-id="ec8fb-108">В этой статье показано, как tooset Azure метрики предупреждений с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-108">This article shows you how tooset up Azure metric alerts using hello Azure portal.</span></span>   

<span data-ttu-id="ec8fb-109">Вы можете получать оповещения на основе отслеживания метрик или событий в службах Azure.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="ec8fb-110">**Значения метрик** - hello предупредить триггеры hello значение указанной метрики пересекает пороговое значение, присваиваемое в любом направлении.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="ec8fb-111">То есть, и триггеров при hello сначала условия, и затем позже при, условия больше не выполнены.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="ec8fb-112">**События журнала действий**. Оповещение может активироваться при *каждом* событии или только тогда, когда выполняются определенные события.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="ec8fb-113">Дополнительные сведения об активности журнала предупреждений toolearn [щелкните здесь](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="ec8fb-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="ec8fb-114">Вы можете настроить метрики оповещений toodo hello следующие при инициировании:</span><span class="sxs-lookup"><span data-stu-id="ec8fb-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="ec8fb-115">Отправить администратору службы toohello уведомлений электронной почты и соадминистраторы</span><span class="sxs-lookup"><span data-stu-id="ec8fb-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="ec8fb-116">Отправьте по электронной почте tooadditional сообщений электронной почты, указанных вами.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="ec8fb-117">вызов webhook;</span><span class="sxs-lookup"><span data-stu-id="ec8fb-117">call a webhook</span></span>
* <span data-ttu-id="ec8fb-118">Запустите выполнение runbook для Azure (только из hello портал Azure)</span><span class="sxs-lookup"><span data-stu-id="ec8fb-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="ec8fb-119">Для настройки правил генерации оповещений метрик и получении сведений о них можно использовать:</span><span class="sxs-lookup"><span data-stu-id="ec8fb-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="ec8fb-120">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ec8fb-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="ec8fb-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec8fb-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="ec8fb-122">интерфейс командной строки (CLI)</span><span class="sxs-lookup"><span data-stu-id="ec8fb-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="ec8fb-123">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="ec8fb-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a><span data-ttu-id="ec8fb-124">Создать правило генерации оповещений на метрики с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ec8fb-124">Create an alert rule on a metric with hello Azure portal</span></span>
1. <span data-ttu-id="ec8fb-125">В hello [портала](https://portal.azure.com/)вас интересуют мониторинг ресурсов hello найдите и выберите его.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-125">In hello [portal](https://portal.azure.com/), locate hello resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="ec8fb-126">Выберите **оповещения** или **предупреждения правила** под hello МОНИТОРИНГ раздела.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-126">Select **Alerts** or **Alert rules** under hello MONITORING section.</span></span> <span data-ttu-id="ec8fb-127">текст Hello и значок, могут немного отличаться для разных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-127">hello text and icon may vary slightly for different resources.</span></span>  

    ![Мониторинг](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="ec8fb-129">Выберите hello **добавить оповещение** команды и заполните поля hello.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-129">Select hello **Add alert** command and fill in hello fields.</span></span>

    ![Добавить оповещение](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="ec8fb-131">Введите **имя** правила генерации оповещений и укажите **описание**, отображаемое также в уведомлениях по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="ec8fb-132">Выберите hello **метрика** toomonitor и нажмите кнопку **условие** и **пороговое значение** значение метрики hello.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-132">Select hello **Metric** you want toomonitor, then choose a **Condition** and **Threshold** value for hello metric.</span></span> <span data-ttu-id="ec8fb-133">Также флажок hello **период** hello метрику времени правила должны соблюдаться hello предупреждения триггеры.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-133">Also chose hello **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span> <span data-ttu-id="ec8fb-134">Например при использовании hello период «PT5M» и оповещения ищет ЦП превышает 80%, hello предупреждение срабатывает при hello ЦП был постоянно выше 80% 5 минут.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-134">So for example, if you use hello period "PT5M" and your alert looks for CPU above 80%, hello alert triggers when hello CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="ec8fb-135">При возникновении hello первый триггер, снова запускает при hello ЦП будет ниже 80% в течение 5 минут.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-135">Once hello first trigger occurs, it again triggers when hello CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="ec8fb-136">Hello измерения ЦП происходит каждую минуту.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-136">hello CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="ec8fb-137">Проверьте **электронной почты владельцев...**  при необходимости администраторы и соадминистраторы toobe по электронной почте hello оповещений активируется.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-137">Check **Email owners...** if you want administrators and co-administrators toobe emailed when hello alert fires.</span></span>

7. <span data-ttu-id="ec8fb-138">Если дополнительные сообщения электронной почты tooreceive уведомление, когда hello срабатывает предупреждение, добавьте их в hello **email(s) дополнительного администратора** поля.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-138">If you want additional emails tooreceive a notification when hello alert fires, add them in hello **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="ec8fb-139">При указании нескольких электронных адресов разделите их точкой с запятой: *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="ec8fb-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="ec8fb-140">Поместите в допустимый URI hello **веб-перехватчика** поле при необходимости его вызывается при hello оповещений активируется.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-140">Put in a valid URI in hello **Webhook** field if you want it called when hello alert fires.</span></span>

9. <span data-ttu-id="ec8fb-141">Если вы используете службы автоматизации Azure, можно выбрать toobe Runbook, при выводе предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-141">If you use Azure Automation, you can select a Runbook toobe run when hello alert fires.</span></span>

10. <span data-ttu-id="ec8fb-142">Выберите **ОК** при done toocreate hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-142">Select **OK** when done toocreate hello alert.</span></span>   

<span data-ttu-id="ec8fb-143">В течение нескольких минут hello предупреждения является активным и триггеры, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-143">Within a few minutes, hello alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="ec8fb-144">Управление оповещениями</span><span class="sxs-lookup"><span data-stu-id="ec8fb-144">Managing your alerts</span></span>
<span data-ttu-id="ec8fb-145">После создания оповещение можно выбрать и:</span><span class="sxs-lookup"><span data-stu-id="ec8fb-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="ec8fb-146">Просмотрите диаграмму, показывающую пороговое значение метрики hello и фактическими значениями hello из hello предыдущий день.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-146">View a graph showing hello metric threshold and hello actual values from hello previous day.</span></span>
* <span data-ttu-id="ec8fb-147">изменить или удалить его;</span><span class="sxs-lookup"><span data-stu-id="ec8fb-147">Edit or delete it.</span></span>
* <span data-ttu-id="ec8fb-148">**Отключить** или **включить** его, если вы желаете tootemporarily остановить или возобновить получение уведомлений для данного предупреждения.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-148">**Disable** or **Enable** it if you want tootemporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec8fb-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec8fb-149">Next steps</span></span>
* <span data-ttu-id="ec8fb-150">[Обзор мониторинг Azure](monitoring-overview.md) включая hello типы данных, можно собирать и контролировать.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-150">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="ec8fb-151">Узнайте больше о [настройке веб-перехватчиков webhook в оповещениях](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ec8fb-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="ec8fb-152">Узнайте больше о [настройке оповещений о событиях журнала действий](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ec8fb-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="ec8fb-153">Узнайте больше о [модулях Runbook службы автоматизации Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="ec8fb-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="ec8fb-154">Ознакомьтесь с [обзором журналов диагностики](monitoring-overview-of-diagnostic-logs.md) , чтобы собирать подробные метрики о службе с высокой частотой.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="ec8fb-155">Получить [Обзор сбора метрик](insights-how-to-customize-monitoring.md) toomake убедиться, что служба становится доступной и отвечать на запросы.</span><span class="sxs-lookup"><span data-stu-id="ec8fb-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
