---
title: "Образец aaaWebhook действие предупреждения в аналитику журнала OMS | Документы Microsoft"
description: "Одно из действий hello, можно запустить в ответ tooa предупреждение анализа журналов — * веб-перехватчика *, позволяющий tooinvoke внешний процесс через один HTTP-запроса. В этой статье рассматривается пример создания действия webhook в оповещении Log Analytics с использованием Slack."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a><span data-ttu-id="0a353-104">Создание предупреждения веб-перехватчика действия в tooSlack сообщения toosend анализа журналов OMS</span><span class="sxs-lookup"><span data-stu-id="0a353-104">Create an alert webhook action in OMS Log Analytics toosend message tooSlack</span></span>
<span data-ttu-id="0a353-105">Одно из действий hello, можно запустить в ответ tooa [предупреждение анализа журналов](log-analytics-alerts.md) — *веб-перехватчика*, позволяющее tooinvoke внешний процесс через один HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="0a353-105">One of hello actions you can run in response tooa [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you tooinvoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="0a353-106">Подробные сведения об оповещениях и действиях webhook см. в статье [Оповещения в Log Analytics](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="0a353-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="0a353-107">В этой статье рассматривается пример создания действия webhook в оповещении Log Analytics с использованием службы обмена сообщениями Slack.</span><span class="sxs-lookup"><span data-stu-id="0a353-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="0a353-108">В этом примере необходимо иметь toocomplete учетная запись Slack.</span><span class="sxs-lookup"><span data-stu-id="0a353-108">You must have a Slack account toocomplete this sample.</span></span>  <span data-ttu-id="0a353-109">Ее можно получить бесплатно на сайте [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="0a353-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="0a353-110">Шаг 1. Включение действий webhook в Slack</span><span class="sxs-lookup"><span data-stu-id="0a353-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="0a353-111">Войдите в tooSlack на [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="0a353-111">Sign in tooSlack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="0a353-112">Выберите канал в hello **каналы** hello левой области.</span><span class="sxs-lookup"><span data-stu-id="0a353-112">Select a channel in hello **Channels** section in hello left pane.</span></span>  <span data-ttu-id="0a353-113">Это hello канала будет отправляться сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="0a353-113">This is hello channel that hello message will be sent to.</span></span>  <span data-ttu-id="0a353-114">Выберите один из каналов по умолчанию hello например **Общие** или **случайных**.</span><span class="sxs-lookup"><span data-stu-id="0a353-114">You can select one of hello default channels such as **general** or **random**.</span></span>  <span data-ttu-id="0a353-115">В рабочих сценариях чаще всего создается специальный канал, например **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="0a353-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Каналы Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="0a353-117">Нажмите кнопку **добавить приложения или индивидуальная настройка** tooopen hello каталога приложения.</span><span class="sxs-lookup"><span data-stu-id="0a353-117">Click **Add an app or custom integration** tooopen hello App Directory.</span></span>
4. <span data-ttu-id="0a353-118">Тип *веб-перехватчиков* в поле поиска hello, а затем выберите **входящего веб-перехватчиков**.</span><span class="sxs-lookup"><span data-stu-id="0a353-118">Type *webhooks* into hello search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Каналы Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="0a353-120">Нажмите кнопку **установить** следующее имя команды tooyour.</span><span class="sxs-lookup"><span data-stu-id="0a353-120">Click **Install** next tooyour team name.</span></span>
6. <span data-ttu-id="0a353-121">Щелкните **Add Configuration**(Добавить конфигурацию).</span><span class="sxs-lookup"><span data-stu-id="0a353-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="0a353-122">Выберите hello hello канала будем toouse для этого примера и нажмите кнопку **интеграции Добавление входящего веб-перехватчиков**.</span><span class="sxs-lookup"><span data-stu-id="0a353-122">Select hello hello channel that you're going toouse for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="0a353-123">Копировать hello **URL-адрес веб-перехватчика**.</span><span class="sxs-lookup"><span data-stu-id="0a353-123">Copy hello **Webhook URL**.</span></span>  <span data-ttu-id="0a353-124">Вы сможете вставить это в конфигурации оповещений hello.</span><span class="sxs-lookup"><span data-stu-id="0a353-124">You'll be pasting this into hello Alert configuration.</span></span> <br>
   
    ![Каналы Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="0a353-126">Шаг 2. Создание правила генерации оповещений в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0a353-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="0a353-127">[Создать правило оповещения](log-analytics-alerts.md) с hello следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="0a353-127">[Create an alert rule](log-analytics-alerts.md) with hello following settings.</span></span>
   * <span data-ttu-id="0a353-128">Запрос: ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="0a353-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="0a353-129">Check for this alert every: 5 minutes (Проверять это оповещение: каждые 5 минут)</span><span class="sxs-lookup"><span data-stu-id="0a353-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="0a353-130">Hello количество результатов: больше 10</span><span class="sxs-lookup"><span data-stu-id="0a353-130">hello number of results is: greater than 10</span></span>
   * <span data-ttu-id="0a353-131">Over this time window: 60 minutes (За период: 60 минут)</span><span class="sxs-lookup"><span data-stu-id="0a353-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="0a353-132">Выберите **Да** для **веб-перехватчика** и **нет** для hello других действий.</span><span class="sxs-lookup"><span data-stu-id="0a353-132">Select **Yes** for **Webhook** and **No** for hello other actions.</span></span>
2. <span data-ttu-id="0a353-133">Вставить hello URL-адрес Slack в hello **URL-адрес веб-перехватчика** поля.</span><span class="sxs-lookup"><span data-stu-id="0a353-133">Paste hello Slack URL into hello **Webhook URL** field.</span></span>
3. <span data-ttu-id="0a353-134">Выберите параметр hello слишком**включить настраиваемые полезные данные JSON**.</span><span class="sxs-lookup"><span data-stu-id="0a353-134">Select hello option too**include a custom JSON payload**.</span></span>
4. <span data-ttu-id="0a353-135">Slack ожидает полезные данные в формате JSON с параметром *text*.</span><span class="sxs-lookup"><span data-stu-id="0a353-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="0a353-136">Это текст hello, которые будут отображаться в приветственное сообщение, он создает.</span><span class="sxs-lookup"><span data-stu-id="0a353-136">This is hello text that it will display in hello message it creates.</span></span>  <span data-ttu-id="0a353-137">Можно использовать один или несколько параметров hello предупреждений с помощью hello  *#*  символов, таких как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="0a353-137">You can use one or more of hello alert parameters using hello *#* symbol such as in hello following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![пример полезных данных JSON](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="0a353-139">Нажмите кнопку **Сохранить** правило оповещения toosave hello.</span><span class="sxs-lookup"><span data-stu-id="0a353-139">Click **Save** toosave hello alert rule.</span></span>
6. <span data-ttu-id="0a353-140">Подождите достаточное время для оповещения toobe создан и проверьте для сообщения, которое будет иметь примерно следующий toohello Slack.</span><span class="sxs-lookup"><span data-stu-id="0a353-140">Wait sufficient time for an alert toobe created and then check Slack for a message which will be similar toohello following.</span></span>
   
   ![пример webhook в Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="0a353-142">Расширенные полезные данные webhook для Slack</span><span class="sxs-lookup"><span data-stu-id="0a353-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="0a353-143">Slack позволяет настроить входные сообщения в широких пределах.</span><span class="sxs-lookup"><span data-stu-id="0a353-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="0a353-144">Дополнительные сведения см. в разделе [входящего веб-перехватчиков](https://api.slack.com/incoming-webhooks) резерв hello веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="0a353-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on hello Slack website.</span></span> <span data-ttu-id="0a353-145">Ниже приведен более сложные toocreate полезных данных форматированного сообщения с форматированием.</span><span class="sxs-lookup"><span data-stu-id="0a353-145">Following is a more complex payload toocreate a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


<span data-ttu-id="0a353-146">Это вызовет сообщение в резерв аналогичные toohello ниже.</span><span class="sxs-lookup"><span data-stu-id="0a353-146">This would generate a message in Slack similar toohello following.</span></span>

![пример сообщения в Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="0a353-148">Сводка</span><span class="sxs-lookup"><span data-stu-id="0a353-148">Summary</span></span>
<span data-ttu-id="0a353-149">С помощью этого правила оповещения в месте tooSlack сообщение, отправленное бы каждый раз hello условий.</span><span class="sxs-lookup"><span data-stu-id="0a353-149">With this alert rule in place, you would have a message sent tooSlack every time hello criteria is met.</span></span>  

<span data-ttu-id="0a353-150">Это только один пример действия, которые можно создавать в предупреждении tooan ответа.</span><span class="sxs-lookup"><span data-stu-id="0a353-150">This is only one example of an action that you can create in response tooan alert.</span></span>  <span data-ttu-id="0a353-151">Можно создать веб-перехватчика действие, которое вызывает другой внешней службы, действие runbook toostart runbook в автоматизации Azure или toosend действия электронной почты tooyourself почты или другим получателям.</span><span class="sxs-lookup"><span data-stu-id="0a353-151">You could create a webhook action that calls another external service, a runbook action toostart a runbook in Azure Automation, or an email action toosend a mail tooyourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="0a353-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a353-152">Next Steps</span></span>
* <span data-ttu-id="0a353-153">Дополнительные сведения о [действиях оповещения в Log Analytics](log-analytics-alerts-actions.md), включая другие действия.</span><span class="sxs-lookup"><span data-stu-id="0a353-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


