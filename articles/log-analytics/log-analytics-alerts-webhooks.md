---
title: "Пример действия webhook для оповещения в OMS Log Analytics | Документация Майкрософт"
description: "Одно из действий, которое можно выполнить в ответ на оповещение Log Analytics, — это webhook. Оно позволяет вызвать внешний процесс посредством одного HTTP-запроса. В этой статье рассматривается пример создания действия webhook в оповещении Log Analytics с использованием Slack."
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
ms.openlocfilehash: 55b66132f7ec5c26c0a7cac1ec0a5c403dbd1082
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-to-send-message-to-slack"></a><span data-ttu-id="fee60-104">Создание действия webhook для оповещения в OMS Log Analytics для отправки сообщения в Slack</span><span class="sxs-lookup"><span data-stu-id="fee60-104">Create an alert webhook action in OMS Log Analytics to send message to Slack</span></span>
<span data-ttu-id="fee60-105">Одно из действий, которое можно выполнить в ответ на оповещение [Log Analytics](log-analytics-alerts.md), — это *webhook*. Оно позволяет вызвать внешний процесс посредством одного HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="fee60-105">One of the actions you can run in response to a [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you to invoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="fee60-106">Подробные сведения об оповещениях и действиях webhook см. в статье [Оповещения в Log Analytics](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="fee60-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="fee60-107">В этой статье рассматривается пример создания действия webhook в оповещении Log Analytics с использованием службы обмена сообщениями Slack.</span><span class="sxs-lookup"><span data-stu-id="fee60-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="fee60-108">Для работы этим с примером требуется учетная запись Slack.</span><span class="sxs-lookup"><span data-stu-id="fee60-108">You must have a Slack account to complete this sample.</span></span>  <span data-ttu-id="fee60-109">Ее можно получить бесплатно на сайте [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="fee60-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="fee60-110">Шаг 1. Включение действий webhook в Slack</span><span class="sxs-lookup"><span data-stu-id="fee60-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="fee60-111">Войдите в службу Slack по адресу [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="fee60-111">Sign in to Slack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="fee60-112">Выберите канал в разделе **Channels** (Каналы) в левой области.</span><span class="sxs-lookup"><span data-stu-id="fee60-112">Select a channel in the **Channels** section in the left pane.</span></span>  <span data-ttu-id="fee60-113">Это канал, в который будет отправлено сообщение.</span><span class="sxs-lookup"><span data-stu-id="fee60-113">This is the channel that the message will be sent to.</span></span>  <span data-ttu-id="fee60-114">Можно выбрать один из каналов по умолчанию, например **general** или **random**.</span><span class="sxs-lookup"><span data-stu-id="fee60-114">You can select one of the default channels such as **general** or **random**.</span></span>  <span data-ttu-id="fee60-115">В рабочих сценариях чаще всего создается специальный канал, например **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="fee60-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Каналы Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="fee60-117">Щелкните **Add an app or custom integration** (Добавить приложение или настраиваемую интеграцию) для открытия каталога приложений.</span><span class="sxs-lookup"><span data-stu-id="fee60-117">Click **Add an app or custom integration** to open the App Directory.</span></span>
4. <span data-ttu-id="fee60-118">Введите *webhooks* в поле поиска, а затем выберите **Incoming WebHooks**(Входящие webhook).</span><span class="sxs-lookup"><span data-stu-id="fee60-118">Type *webhooks* into the search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Каналы Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="fee60-120">Щелкните элемент **Install** (Установить) рядом с именем группы.</span><span class="sxs-lookup"><span data-stu-id="fee60-120">Click **Install** next to your team name.</span></span>
6. <span data-ttu-id="fee60-121">Щелкните **Add Configuration**(Добавить конфигурацию).</span><span class="sxs-lookup"><span data-stu-id="fee60-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="fee60-122">Выберите канал, который вы собираетесь использовать для этого примера, и щелкните **Add Incoming WebHooks integration**(Добавить интеграцию входящих webhook).</span><span class="sxs-lookup"><span data-stu-id="fee60-122">Select the the channel that you're going to use for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="fee60-123">Скопируйте значение **Webhook URL**(URL-адрес webhook).</span><span class="sxs-lookup"><span data-stu-id="fee60-123">Copy the **Webhook URL**.</span></span>  <span data-ttu-id="fee60-124">Его потребуется вставить в конфигурацию оповещения.</span><span class="sxs-lookup"><span data-stu-id="fee60-124">You'll be pasting this into the Alert configuration.</span></span> <br>
   
    ![Каналы Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="fee60-126">Шаг 2. Создание правила генерации оповещений в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="fee60-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="fee60-127">[Создайте правило генерации оповещений](log-analytics-alerts.md) со приведенными ниже параметрами.</span><span class="sxs-lookup"><span data-stu-id="fee60-127">[Create an alert rule](log-analytics-alerts.md) with the following settings.</span></span>
   * <span data-ttu-id="fee60-128">Запрос: ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="fee60-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="fee60-129">Check for this alert every: 5 minutes (Проверять это оповещение: каждые 5 минут)</span><span class="sxs-lookup"><span data-stu-id="fee60-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="fee60-130">The number of results is: greater than 10 (Количество результатов: больше 10)</span><span class="sxs-lookup"><span data-stu-id="fee60-130">The number of results is: greater than 10</span></span>
   * <span data-ttu-id="fee60-131">Over this time window: 60 minutes (За период: 60 минут)</span><span class="sxs-lookup"><span data-stu-id="fee60-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="fee60-132">Выберите **Yes** (Да) для **Webhook** и **No** (Нет) для других действий.</span><span class="sxs-lookup"><span data-stu-id="fee60-132">Select **Yes** for **Webhook** and **No** for the other actions.</span></span>
2. <span data-ttu-id="fee60-133">Вставьте URL-адрес Slack в поле **Webhook URL** (URL-адрес webhook).</span><span class="sxs-lookup"><span data-stu-id="fee60-133">Paste the Slack URL into the **Webhook URL** field.</span></span>
3. <span data-ttu-id="fee60-134">Выберите параметр **Include custom JSON payload**(Включить настраиваемые полезные данные JSON).</span><span class="sxs-lookup"><span data-stu-id="fee60-134">Select the option to **include a custom JSON payload**.</span></span>
4. <span data-ttu-id="fee60-135">Slack ожидает полезные данные в формате JSON с параметром *text*.</span><span class="sxs-lookup"><span data-stu-id="fee60-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="fee60-136">Это текст, который отображается в создаваемом сообщении.</span><span class="sxs-lookup"><span data-stu-id="fee60-136">This is the text that it will display in the message it creates.</span></span>  <span data-ttu-id="fee60-137">Можно использовать один или несколько параметров оповещения с помощью символа *#* , как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="fee60-137">You can use one or more of the alert parameters using the *#* symbol such as in the following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds the over threshold of #thresholdvalue ."
    }
    ```
   
    ![пример полезных данных JSON](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="fee60-139">Щелкните **Save** (Сохранить), чтобы сохранить правило генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="fee60-139">Click **Save** to save the alert rule.</span></span>
6. <span data-ttu-id="fee60-140">Подождите достаточное время для создания оповещения и проверьте, появилось ли в Slack сообщение, аналогичное следующему.</span><span class="sxs-lookup"><span data-stu-id="fee60-140">Wait sufficient time for an alert to be created and then check Slack for a message which will be similar to the following.</span></span>
   
   ![пример webhook в Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="fee60-142">Расширенные полезные данные webhook для Slack</span><span class="sxs-lookup"><span data-stu-id="fee60-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="fee60-143">Slack позволяет настроить входные сообщения в широких пределах.</span><span class="sxs-lookup"><span data-stu-id="fee60-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="fee60-144">Дополнительные сведения см. в статье [Incoming Webhooks](https://api.slack.com/incoming-webhooks) (Входящие webhook) на веб-сайте Slack.</span><span class="sxs-lookup"><span data-stu-id="fee60-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on the Slack website.</span></span> <span data-ttu-id="fee60-145">Ниже приведены более сложные полезные данные для создания сообщения с форматированием.</span><span class="sxs-lookup"><span data-stu-id="fee60-145">Following is a more complex payload to create a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link To SearchResults",
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


<span data-ttu-id="fee60-146">При этом в Slack создается сообщение, аналогичное следующему.</span><span class="sxs-lookup"><span data-stu-id="fee60-146">This would generate a message in Slack similar to the following.</span></span>

![пример сообщения в Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="fee60-148">Сводка</span><span class="sxs-lookup"><span data-stu-id="fee60-148">Summary</span></span>
<span data-ttu-id="fee60-149">После создания этого правила генерации оповещений при каждом соблюдении условий в Slack должно отправляться сообщение.</span><span class="sxs-lookup"><span data-stu-id="fee60-149">With this alert rule in place, you would have a message sent to Slack every time the criteria is met.</span></span>  

<span data-ttu-id="fee60-150">Это лишь один пример действия, которое можно создать в ответ на оповещение.</span><span class="sxs-lookup"><span data-stu-id="fee60-150">This is only one example of an action that you can create in response to an alert.</span></span>  <span data-ttu-id="fee60-151">Можно создать действие webhook, которое вызывает другую внешнюю службу, действие Runbook, чтобы запустить модуль Runbook в службе автоматизации Azure, или действие электронной почты для отправки сообщения себе или другим получателям.</span><span class="sxs-lookup"><span data-stu-id="fee60-151">You could create a webhook action that calls another external service, a runbook action to start a runbook in Azure Automation, or an email action to send a mail to yourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="fee60-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fee60-152">Next Steps</span></span>
* <span data-ttu-id="fee60-153">Дополнительные сведения о [действиях оповещения в Log Analytics](log-analytics-alerts-actions.md), включая другие действия.</span><span class="sxs-lookup"><span data-stu-id="fee60-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


