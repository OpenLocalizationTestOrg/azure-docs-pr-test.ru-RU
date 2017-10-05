---
title: "Ответ на оповещение в OMS Log Analytics | Документация Майкрософт"
description: "Оповещения в Log Analytics идентифицируют важную информацию в репозитории OMS и могут заранее уведомлять вас о возникших проблемах или выполнять действия в попытке устранить их.  Эта статья описывает создание правила генерации оповещений и сведения о различных действиях, которые оно может выполнить."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b8731e1fe48b7d809b113eb5273e3962542b8f34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-actions-to-alert-rules-in-log-analytics"></a><span data-ttu-id="320de-104">Добавление действий в правила оповещений в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="320de-104">Add actions to alert rules in Log Analytics</span></span>
<span data-ttu-id="320de-105">При [создании оповещения в Log Analytics](log-analytics-alerts.md) можно [настроить правила оповещений](log-analytics-alerts.md) для выполнения одного или нескольких действий.</span><span class="sxs-lookup"><span data-stu-id="320de-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have the option of [configuring the alert rule](log-analytics-alerts.md) to perform one or more actions.</span></span>  <span data-ttu-id="320de-106">В этой статье описываются различные доступные действия и сведения о том, как их настроить.</span><span class="sxs-lookup"><span data-stu-id="320de-106">This article describes the different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="320de-107">Действие</span><span class="sxs-lookup"><span data-stu-id="320de-107">Action</span></span> | <span data-ttu-id="320de-108">Описание</span><span class="sxs-lookup"><span data-stu-id="320de-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="320de-109">Электронная почта</span><span class="sxs-lookup"><span data-stu-id="320de-109">Email</span></span>](#email-actions) | <span data-ttu-id="320de-110">Отправка сообщения электронной почты с описанием оповещения одному или нескольким получателям.</span><span class="sxs-lookup"><span data-stu-id="320de-110">Send an e-mail with the details of the alert to one or more recipients.</span></span> |
| [<span data-ttu-id="320de-111">webhook</span><span class="sxs-lookup"><span data-stu-id="320de-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="320de-112">Вызов внешнего процесса с помощью одного запроса HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="320de-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="320de-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="320de-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="320de-114">Запуск модуля Runbook в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="320de-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="320de-115">Действия электронной почты</span><span class="sxs-lookup"><span data-stu-id="320de-115">Email actions</span></span>
<span data-ttu-id="320de-116">Действия электронной почты отправляют сообщение электронной почты с описанием оповещения одному или несколькими получателям.</span><span class="sxs-lookup"><span data-stu-id="320de-116">Email actions send an e-mail with the details of the alert to one or more recipients.</span></span>  <span data-ttu-id="320de-117">Вы можете указать тему сообщения, но его содержимое имеет стандартный формат, определяемый службой Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="320de-117">You can specify the subject of the mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="320de-118">Оно содержит сводные данные, такие как имя оповещения, а также описание до 10 записей, возвращенных в результате поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="320de-118">It includes summary information such as the name of the alert in addition to details of up to ten records returned by the log search.</span></span>  <span data-ttu-id="320de-119">Он также включает ссылку на поиск журналов в Log Analytics, которая возвращает полный набор записей на основе этого запроса.</span><span class="sxs-lookup"><span data-stu-id="320de-119">It also includes a link to a log search in Log Analytics that will return the entire set of records from that query.</span></span>   <span data-ttu-id="320de-120">Отправителем сообщения является *группа разработчиков Microsoft Operations Management Suite&lt;noreply@oms.microsoft.com&gt;*.</span><span class="sxs-lookup"><span data-stu-id="320de-120">The sender of the mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="320de-121">Для выполнения действий электронной почты требуются свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="320de-121">Email actions require the properties in the following table.</span></span>

| <span data-ttu-id="320de-122">Свойство</span><span class="sxs-lookup"><span data-stu-id="320de-122">Property</span></span> | <span data-ttu-id="320de-123">Описание</span><span class="sxs-lookup"><span data-stu-id="320de-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="320de-124">Субъект</span><span class="sxs-lookup"><span data-stu-id="320de-124">Subject</span></span> |<span data-ttu-id="320de-125">Тема сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="320de-125">Subject in the email.</span></span>  <span data-ttu-id="320de-126">Основной текст сообщения нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="320de-126">You cannot modify the body of the mail.</span></span> |
| <span data-ttu-id="320de-127">Recipients</span><span class="sxs-lookup"><span data-stu-id="320de-127">Recipients</span></span> |<span data-ttu-id="320de-128">Адреса всех получателей электронной почты.</span><span class="sxs-lookup"><span data-stu-id="320de-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="320de-129">При указании нескольких адресов разделяйте их точкой с запятой (;).</span><span class="sxs-lookup"><span data-stu-id="320de-129">If you specify more than one address, then separate the addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="320de-130">Действия webhook</span><span class="sxs-lookup"><span data-stu-id="320de-130">Webhook actions</span></span>

<span data-ttu-id="320de-131">Действия webhook позволяют вызывать внешний процесс с помощью одного запроса HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="320de-131">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="320de-132">Вызываемая служба должна поддерживать действия webhook и определить использование получаемых полезных данных.</span><span class="sxs-lookup"><span data-stu-id="320de-132">The service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="320de-133">Можно также вызвать REST API без поддержки действий webhook, если запрос имеет формат, понятный этому API.</span><span class="sxs-lookup"><span data-stu-id="320de-133">You could also call a REST API that doesn't specifically support webhooks as long as the request is in a format that the API understands.</span></span>  <span data-ttu-id="320de-134">Примеры использования webhook в ответ на оповещение включают в себя отправку сообщения в [Slack](http://slack.com) или создание инцидента в [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="320de-134">Examples of using a webhook in response to an alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="320de-135">Полное пошаговое руководство по созданию правила генерации оповещений с webhook для вызова Slack см. в статье [Действия webhook в оповещениях Log Analytics](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="320de-135">A complete walkthrough of creating an alert rule with a webhook to call Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="320de-136">Для выполнения действий webhook требуются свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="320de-136">Webhook actions require the properties in the following table.</span></span>

| <span data-ttu-id="320de-137">Свойство</span><span class="sxs-lookup"><span data-stu-id="320de-137">Property</span></span> | <span data-ttu-id="320de-138">Описание</span><span class="sxs-lookup"><span data-stu-id="320de-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="320de-139">URL-адрес Webhook</span><span class="sxs-lookup"><span data-stu-id="320de-139">Webhook URL</span></span> |<span data-ttu-id="320de-140">URL-адрес действия webhook.</span><span class="sxs-lookup"><span data-stu-id="320de-140">The URL of the webhook.</span></span> |
| <span data-ttu-id="320de-141">Настраиваемые полезные данные JSON</span><span class="sxs-lookup"><span data-stu-id="320de-141">Custom JSON payload</span></span> |<span data-ttu-id="320de-142">Настраиваемые полезные данные для отправки с webhook.</span><span class="sxs-lookup"><span data-stu-id="320de-142">Custom payload to send with the webhook.</span></span>  <span data-ttu-id="320de-143">Дополнительные сведения см. ниже.</span><span class="sxs-lookup"><span data-stu-id="320de-143">See below for details.</span></span> |


<span data-ttu-id="320de-144">Действия webhook включают URL-адрес и полезные данные в формате JSON, которые являются данными, отправляемыми во внешнюю службу.</span><span class="sxs-lookup"><span data-stu-id="320de-144">Webhooks include a URL and a payload formatted in JSON that is the data sent to the external service.</span></span>  <span data-ttu-id="320de-145">По умолчанию полезные данные включают в себя значения из приведенной ниже таблицы.</span><span class="sxs-lookup"><span data-stu-id="320de-145">By default, the payload will include the values in the following table.</span></span>  <span data-ttu-id="320de-146">Такие полезные данные можно заменить на собственные.</span><span class="sxs-lookup"><span data-stu-id="320de-146">You can choose to replace this payload with a custom one of your own.</span></span>  <span data-ttu-id="320de-147">В этом случае можно использовать переменные из таблицы для каждого параметра, чтобы включить их значение в пользовательские полезные данные.</span><span class="sxs-lookup"><span data-stu-id="320de-147">In that case you can use the variables in the table for each of the parameters to include their value in your custom payload.</span></span>

| <span data-ttu-id="320de-148">Параметр</span><span class="sxs-lookup"><span data-stu-id="320de-148">Parameter</span></span> | <span data-ttu-id="320de-149">Переменная</span><span class="sxs-lookup"><span data-stu-id="320de-149">Variable</span></span> | <span data-ttu-id="320de-150">Описание</span><span class="sxs-lookup"><span data-stu-id="320de-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="320de-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="320de-151">AlertRuleName</span></span> |<span data-ttu-id="320de-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="320de-152">#alertrulename</span></span> |<span data-ttu-id="320de-153">Имя правила генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="320de-153">Name of the alert rule.</span></span> |
| <span data-ttu-id="320de-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="320de-154">AlertThresholdOperator</span></span> |<span data-ttu-id="320de-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="320de-155">#thresholdoperator</span></span> |<span data-ttu-id="320de-156">Оператор порога для правила генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="320de-156">Threshold operator for the alert rule.</span></span>  <span data-ttu-id="320de-157">*Больше* или *Меньше*.</span><span class="sxs-lookup"><span data-stu-id="320de-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="320de-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="320de-158">AlertThresholdValue</span></span> |<span data-ttu-id="320de-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="320de-159">#thresholdvalue</span></span> |<span data-ttu-id="320de-160">Значение порога для правила генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="320de-160">Threshold value for the alert rule.</span></span> |
| <span data-ttu-id="320de-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="320de-161">LinkToSearchResults</span></span> |<span data-ttu-id="320de-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="320de-162">#linktosearchresults</span></span> |<span data-ttu-id="320de-163">Ссылки на поиск журналов Log Analytics, возвращающая записи из запроса, создавшего оповещение.</span><span class="sxs-lookup"><span data-stu-id="320de-163">Link to Log Analytics log search that returns the records from the query that created the alert.</span></span> |
| <span data-ttu-id="320de-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="320de-164">ResultCount</span></span> |<span data-ttu-id="320de-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="320de-165">#searchresultcount</span></span> |<span data-ttu-id="320de-166">Число записей в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="320de-166">Number of records in the search results.</span></span> |
| <span data-ttu-id="320de-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="320de-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="320de-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="320de-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="320de-169">Время окончания для запроса в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="320de-169">End time for the query in UTC format.</span></span> |
| <span data-ttu-id="320de-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="320de-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="320de-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="320de-171">#searchinterval</span></span> |<span data-ttu-id="320de-172">Временное окно для правила генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="320de-172">Time window for the alert rule.</span></span> |
| <span data-ttu-id="320de-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="320de-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="320de-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="320de-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="320de-175">Время начала для запроса в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="320de-175">Start time for the query in UTC format.</span></span> |
| <span data-ttu-id="320de-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="320de-176">SearchQuery</span></span> |<span data-ttu-id="320de-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="320de-177">#searchquery</span></span> |<span data-ttu-id="320de-178">Запрос поиска журналов, используемый правилом генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="320de-178">Log search query used by the alert rule.</span></span> |
| <span data-ttu-id="320de-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="320de-179">SearchResults</span></span> |<span data-ttu-id="320de-180">См. ниже</span><span class="sxs-lookup"><span data-stu-id="320de-180">See below</span></span> |<span data-ttu-id="320de-181">Записи, возвращенные запросом в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="320de-181">Records returned by the query in JSON format.</span></span>  <span data-ttu-id="320de-182">Только первые 5000 записей.</span><span class="sxs-lookup"><span data-stu-id="320de-182">Limited to the first 5,000 records.</span></span> |
| <span data-ttu-id="320de-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="320de-183">WorkspaceID</span></span> |<span data-ttu-id="320de-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="320de-184">#workspaceid</span></span> |<span data-ttu-id="320de-185">Идентификатор рабочей области OMS</span><span class="sxs-lookup"><span data-stu-id="320de-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="320de-186">Например, можно указать следующие пользовательские полезные данные, содержащие один параметр — *text*.</span><span class="sxs-lookup"><span data-stu-id="320de-186">For example, you might specify the following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="320de-187">Служба, вызываемая этим действием webhook, будет ожидать этот параметр.</span><span class="sxs-lookup"><span data-stu-id="320de-187">The service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="320de-188">При отправке в webhook этот пример полезных данных разрешается в нечто следующее:</span><span class="sxs-lookup"><span data-stu-id="320de-188">This example payload would resolve to something like the following when sent to the webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="320de-189">Чтобы включить результаты поиска в пользовательские полезные данные, добавьте следующую строку как свойство верхнего уровня в полезных данных JSON.</span><span class="sxs-lookup"><span data-stu-id="320de-189">To include search results in a custom payload, add the following line as a top level property in the json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="320de-190">Например, чтобы создать пользовательские полезные данные, включающие только имя оповещения и результаты поиска, можно использовать следующее:</span><span class="sxs-lookup"><span data-stu-id="320de-190">For example, to create a custom payload that includes just the alert name and the search results, you could use the following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="320de-191">С полным примером создания правила генерации оповещений с помощью webhook для запуска внешней службы можно ознакомиться в статье [Действия webhook в оповещениях Log Analytics](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="320de-191">You can walk through a complete example of creating an alert rule with a webhook to start an external service at [Create an alert webhook action in OMS Log Analytics to send message to Slack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="320de-192">Действия Runbook</span><span class="sxs-lookup"><span data-stu-id="320de-192">Runbook actions</span></span>
<span data-ttu-id="320de-193">Действия Runbook запускают модуль Runbook в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="320de-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="320de-194">Чтобы использовать этот тип действия, необходимо иметь установленное и настроенное [решение автоматизации](log-analytics-add-solutions.md) в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="320de-194">In order to use this type of action, you must have the [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="320de-195">Можно выбрать один из модулей Runbook в учетной записи автоматизации, настроенной в решении автоматизации.</span><span class="sxs-lookup"><span data-stu-id="320de-195">You can select from the runbooks in the automation account that you configured in the Automation solution.</span></span>

<span data-ttu-id="320de-196">Для выполнения действий Runbook требуются свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="320de-196">Runbook actions require the properties in the following table.</span></span>

| <span data-ttu-id="320de-197">Свойство</span><span class="sxs-lookup"><span data-stu-id="320de-197">Property</span></span> | <span data-ttu-id="320de-198">Описание</span><span class="sxs-lookup"><span data-stu-id="320de-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="320de-199">Модуль Runbook</span><span class="sxs-lookup"><span data-stu-id="320de-199">Runbook</span></span> | <span data-ttu-id="320de-200">Модуль Runbook, который требуется запустить при создании оповещения.</span><span class="sxs-lookup"><span data-stu-id="320de-200">Runbook that you want to start when an alert is created.</span></span> |
| <span data-ttu-id="320de-201">Запуск на</span><span class="sxs-lookup"><span data-stu-id="320de-201">Run on</span></span> | <span data-ttu-id="320de-202">Выберите **Azure** для запуска Runbook в облаке Azure.</span><span class="sxs-lookup"><span data-stu-id="320de-202">Specify **Azure** to run the runbook in the cloud.</span></span>  <span data-ttu-id="320de-203">Выберите **Гибридная рабочая роль** для запуска Runbook в агенте с установленной [гибридной рабочей ролью Runbook](../automation/automation-hybrid-runbook-worker.md ).</span><span class="sxs-lookup"><span data-stu-id="320de-203">Specify **Hybrid worker** to run the runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="320de-204">Действия Runbook запускают модуль Runbook с помощью [webhook](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="320de-204">Runbook actions start the runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="320de-205">При создании правила генерации оповещений автоматически создается новое действие webhook для модуля Runbook с именем **OMS Alert Remediation** , за которым следует GUID.</span><span class="sxs-lookup"><span data-stu-id="320de-205">When you create the alert rule, it will automatically create a new webhook for the runbook with the name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="320de-206">Нельзя напрямую заполнять параметры Runbook. Однако в [параметре $WebhookData](../automation/automation-webhooks.md) будут содержаться подробные сведения о предупреждении, включая результаты поиска по журналам,из-за которого оно возникло.</span><span class="sxs-lookup"><span data-stu-id="320de-206">You cannot directly populate any parameters of the runbook, but the [$WebhookData parameter](../automation/automation-webhooks.md) will include the details of the alert, including the results of the log search that created it.</span></span>  <span data-ttu-id="320de-207">Для доступа к свойствам предупреждения модулю Runbook потребуется определить **$WebhookData** в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="320de-207">The runbook will need to define **$WebhookData** as a parameter for it to access the properties of the alert.</span></span>  <span data-ttu-id="320de-208">Данные предупреждения доступны в формате Json в свойстве **SearchResults** свойства **RequestBody** параметра **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="320de-208">The alert data is available in json format in a single property called **SearchResults** in the **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="320de-209">Свойства этого параметра приведены в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="320de-209">This will have with the properties in the following table.</span></span>

| <span data-ttu-id="320de-210">Узел</span><span class="sxs-lookup"><span data-stu-id="320de-210">Node</span></span> | <span data-ttu-id="320de-211">Описание</span><span class="sxs-lookup"><span data-stu-id="320de-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="320de-212">id</span><span class="sxs-lookup"><span data-stu-id="320de-212">id</span></span> |<span data-ttu-id="320de-213">Путь и GUID для поиска.</span><span class="sxs-lookup"><span data-stu-id="320de-213">Path and GUID of the search.</span></span> |
| <span data-ttu-id="320de-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="320de-214">__metadata</span></span> |<span data-ttu-id="320de-215">Сведения об оповещении, включая количество записей и состояние результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="320de-215">Information about the alert including the number of records and status of the search results.</span></span> |
| <span data-ttu-id="320de-216">value</span><span class="sxs-lookup"><span data-stu-id="320de-216">value</span></span> |<span data-ttu-id="320de-217">Отдельная запись для каждой записи в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="320de-217">Separate entry for each record in the search results.</span></span>  <span data-ttu-id="320de-218">Подробные сведения о записи будут соответствовать свойствам и значениям записи.</span><span class="sxs-lookup"><span data-stu-id="320de-218">The details of the entry will match the properties and values of the record.</span></span> |

<span data-ttu-id="320de-219">Например, следующий модуль Runbook извлечет записи, возвращенные в результате поиска по журналам, и назначит разные свойства на основе типа каждой записи.</span><span class="sxs-lookup"><span data-stu-id="320de-219">For example, the following runbook would extract the records returned by the log search  and assign different properties based on the type of each record.</span></span>  <span data-ttu-id="320de-220">Обратите внимание, что сначала модуль Runbook преобразовывает формат **RequestBody** из Json, чтобы с этим параметром можно было работать в качестве объекта в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="320de-220">Note that the runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a><span data-ttu-id="320de-221">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="320de-221">Next steps</span></span>
- <span data-ttu-id="320de-222">Вы можете выполнить пошаговое руководство по [настройке webook](log-analytics-alerts-webhooks.md) с использованием правила генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="320de-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="320de-223">Вы можете научиться писать [модули Runbook в службе автоматизации Azure](https://azure.microsoft.com/documentation/services/automation) для устранения проблем, обозначенных в оповещениях.</span><span class="sxs-lookup"><span data-stu-id="320de-223">Learn how to write [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) to remediate problems identified by alerts.</span></span>