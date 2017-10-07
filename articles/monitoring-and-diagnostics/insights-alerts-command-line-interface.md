---
title: "оповещения aaaCreate для служб Azure - CLI кросс платформенных | Документы Microsoft"
description: "Триггер сообщения электронной почты, уведомления, вызовите URL-адреса веб-сайтов (веб-перехватчиков) или автоматизации при соблюдении заданных условий hello."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="d511a-103">Создание оповещений метрик в Azure Monitor для служб Azure с помощью кроссплатформенного интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="d511a-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d511a-104">Портал</span><span class="sxs-lookup"><span data-stu-id="d511a-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="d511a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d511a-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="d511a-106">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="d511a-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="d511a-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="d511a-107">Overview</span></span>
<span data-ttu-id="d511a-108">В этой статье показано, как tooset Azure метрики предупреждений с помощью hello кросс платформенных интерфейс командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="d511a-108">This article shows you how tooset up Azure metric alerts using hello cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="d511a-109">Монитор Azure — новое имя hello что был вызван «Azure Insights» до 25 сентября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="d511a-109">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="d511a-110">Однако hello пространств имен и поэтому приведенную ниже команду hello по-прежнему содержать аналитики «hello».</span><span class="sxs-lookup"><span data-stu-id="d511a-110">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
>
>

<span data-ttu-id="d511a-111">Вы можете получать оповещения на основе отслеживания метрик или событий в службах Azure.</span><span class="sxs-lookup"><span data-stu-id="d511a-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="d511a-112">**Значения метрик** - hello предупредить триггеры hello значение указанной метрики пересекает пороговое значение, присваиваемое в любом направлении.</span><span class="sxs-lookup"><span data-stu-id="d511a-112">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="d511a-113">То есть, и триггеров при hello сначала условия, и затем позже при, условия больше не выполнены.</span><span class="sxs-lookup"><span data-stu-id="d511a-113">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="d511a-114">**События журнала действий**. Оповещение может активироваться при *каждом* событии или только тогда, когда выполняются определенные события.</span><span class="sxs-lookup"><span data-stu-id="d511a-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="d511a-115">Дополнительные сведения об активности журнала предупреждений toolearn [щелкните здесь](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="d511a-115">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="d511a-116">Вы можете настроить метрики оповещений toodo hello следующие при инициировании:</span><span class="sxs-lookup"><span data-stu-id="d511a-116">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="d511a-117">Отправить администратору службы toohello уведомлений электронной почты и соадминистраторы</span><span class="sxs-lookup"><span data-stu-id="d511a-117">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="d511a-118">Отправьте по электронной почте tooadditional сообщений электронной почты, указанных вами.</span><span class="sxs-lookup"><span data-stu-id="d511a-118">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="d511a-119">вызов webhook;</span><span class="sxs-lookup"><span data-stu-id="d511a-119">call a webhook</span></span>
* <span data-ttu-id="d511a-120">Запустите выполнение runbook для Azure (только из hello портал Azure в настоящее время)</span><span class="sxs-lookup"><span data-stu-id="d511a-120">start execution of an Azure runbook (only from hello Azure portal at this time)</span></span>

<span data-ttu-id="d511a-121">Для настройки правил генерации оповещений метрик и получении сведений о них можно использовать:</span><span class="sxs-lookup"><span data-stu-id="d511a-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="d511a-122">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d511a-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="d511a-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d511a-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="d511a-124">интерфейс командной строки (CLI)</span><span class="sxs-lookup"><span data-stu-id="d511a-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="d511a-125">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="d511a-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="d511a-126">Всегда можно получать справки для команд с помощью команд и помещения - помочь в конце hello.</span><span class="sxs-lookup"><span data-stu-id="d511a-126">You can always receive help for commands by typing a command and putting -help at hello end.</span></span> <span data-ttu-id="d511a-127">Например:</span><span class="sxs-lookup"><span data-stu-id="d511a-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a><span data-ttu-id="d511a-128">Создание правил оповещений с помощью hello CLI</span><span class="sxs-lookup"><span data-stu-id="d511a-128">Create alert rules using hello CLI</span></span>
1. <span data-ttu-id="d511a-129">Выполните необходимые условия hello и tooAzure входа.</span><span class="sxs-lookup"><span data-stu-id="d511a-129">Perform hello Prerequisites and login tooAzure.</span></span> <span data-ttu-id="d511a-130">См. [примеры CLI для Azure Monitor](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d511a-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="d511a-131">Иными словами установите hello CLI и выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d511a-131">In short, install hello CLI and run these commands.</span></span> <span data-ttu-id="d511a-132">Они вам войти, будет отображена какие подписки используется и подготовки команды toorun монитора Azure.</span><span class="sxs-lookup"><span data-stu-id="d511a-132">They get you logged in, show what subscription you are using, and prepare you toorun Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="d511a-133">toolist существующие правила в группе ресурсов, используйте следующие формы hello **аналитики azure, список правил оповещения** *[параметры] &lt;группа ресурсов&gt;*</span><span class="sxs-lookup"><span data-stu-id="d511a-133">toolist existing rules on a resource group, use hello following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="d511a-134">toocreate правило, требуется toohave несколько важных аспекта сведений сначала.</span><span class="sxs-lookup"><span data-stu-id="d511a-134">toocreate a rule, you need toohave several important pieces of information first.</span></span>
  * <span data-ttu-id="d511a-135">Hello **идентификатор ресурса** для hello ресурса требуется tooset оповещение для</span><span class="sxs-lookup"><span data-stu-id="d511a-135">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="d511a-136">Hello **определения показателей** доступны для этого ресурса</span><span class="sxs-lookup"><span data-stu-id="d511a-136">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="d511a-137">Одним из способов tooget hello идентификатор ресурса — toouse hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d511a-137">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="d511a-138">Предположим, что ресурс hello уже создан, выберите его в портал hello.</span><span class="sxs-lookup"><span data-stu-id="d511a-138">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="d511a-139">Выберите в колонке Далее hello *свойства* под hello *параметры* раздела.</span><span class="sxs-lookup"><span data-stu-id="d511a-139">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="d511a-140">Hello *идентификатор РЕСУРСА* — это поле в колонке Далее hello.</span><span class="sxs-lookup"><span data-stu-id="d511a-140">hello *RESOURCE ID* is a field in hello next blade.</span></span> <span data-ttu-id="d511a-141">Другим способом является toouse hello [обозревателя ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d511a-141">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="d511a-142">Ниже приведен пример идентификатора ресурса для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d511a-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="d511a-143">tooget список доступных показателей hello и единицы измерения для этих метрик для предыдущего примера ресурсов hello, hello используйте следующую команду CLI:</span><span class="sxs-lookup"><span data-stu-id="d511a-143">tooget a list of hello available metrics and units for those metrics for hello previous resource example, use hello following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="d511a-144">*PT1M* — hello гранулярности измерения доступны hello (1-минутные интервалы).</span><span class="sxs-lookup"><span data-stu-id="d511a-144">*PT1M* is hello granularity of hello available measurement (1-minute intervals).</span></span> <span data-ttu-id="d511a-145">Выбор различных уровней детализации позволяет использовать разные параметры метрик.</span><span class="sxs-lookup"><span data-stu-id="d511a-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="d511a-146">toocreate основе метрика правилом оповещений, используйте команду hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="d511a-146">toocreate a metric-based alert rule, use a command of hello following form:</span></span>

    <span data-ttu-id="d511a-147">**azure insights alerts rule metric set** *[параметры] &lt;имя_правила&gt; &lt;расположение&gt; &lt;группа_ресурсов&gt; &lt;размер_окна&gt; &lt;оператор&gt; &lt;пороговое_значение&gt; &lt;ИД_целевого_ресурса&gt; &lt;имя_метрики&gt; &lt;оператор_агрегата_времени&gt;*</span><span class="sxs-lookup"><span data-stu-id="d511a-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="d511a-148">Здравствуйте, следующий пример настраивает оповещение на ресурс веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="d511a-148">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="d511a-149">Hello предупреждения триггеры всякий раз, когда постоянно получает любой трафик, 5 минут, и снова при получении трафика на 5 минут.</span><span class="sxs-lookup"><span data-stu-id="d511a-149">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="d511a-150">toocreate веб-перехватчик или отправить по электронной почте при выводе метрики предупреждения, сначала создайте hello электронной почты и/или веб-привязок.</span><span class="sxs-lookup"><span data-stu-id="d511a-150">toocreate webhook or send email when a metric alert fires, first create hello email and/or webhooks.</span></span> <span data-ttu-id="d511a-151">Создать правило hello немедленно после него.</span><span class="sxs-lookup"><span data-stu-id="d511a-151">Then create hello rule immediately afterwards.</span></span> <span data-ttu-id="d511a-152">Не удалось связать веб-перехватчик или сообщения электронной почты с уже созданные правила, использующие hello CLI.</span><span class="sxs-lookup"><span data-stu-id="d511a-152">You cannot associate webhook or emails with already created rules using hello CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="d511a-153">Можно проверить, правильно ли созданы оповещения, просмотрев отдельное правило.</span><span class="sxs-lookup"><span data-stu-id="d511a-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="d511a-154">правила toodelete команда hello формы:</span><span class="sxs-lookup"><span data-stu-id="d511a-154">toodelete rules, use a command of hello form:</span></span>

    <span data-ttu-id="d511a-155">**insights alerts rule delete** [параметры] &lt;группа_ресурсов&gt; &lt;имя_правила&gt;</span><span class="sxs-lookup"><span data-stu-id="d511a-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="d511a-156">Эти команды удаляют hello правила, созданные ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d511a-156">These commands delete hello rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="d511a-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d511a-157">Next steps</span></span>
* <span data-ttu-id="d511a-158">[Обзор мониторинг Azure](monitoring-overview.md) включая hello типы данных, можно собирать и контролировать.</span><span class="sxs-lookup"><span data-stu-id="d511a-158">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="d511a-159">Узнайте больше о [настройке веб-перехватчиков webhook в оповещениях](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="d511a-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="d511a-160">Узнайте больше о [настройке оповещений о событиях журнала действий](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="d511a-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="d511a-161">Узнайте больше о [модулях Runbook службы автоматизации Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="d511a-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="d511a-162">Получить [Обзор сбора журналов диагностики](monitoring-overview-of-diagnostic-logs.md) toocollect подробные показатели высокой частотой в службе.</span><span class="sxs-lookup"><span data-stu-id="d511a-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="d511a-163">Получить [Обзор сбора метрик](insights-how-to-customize-monitoring.md) toomake убедиться, что служба становится доступной и отвечать на запросы.</span><span class="sxs-lookup"><span data-stu-id="d511a-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
