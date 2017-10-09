---
title: "tooalerts aaaResponses в аналитику журнала OMS | Документы Microsoft"
description: "Предупреждения в службе анализа журналов определить важную информацию в репозитории OMS и можно заранее уведомлять вас о проблемах или вызова действия tooattempt toocorrect их.  В этой статье описывается, как toocreate правила оповещения и сведения о hello различные действия они могут получить."
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
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a><span data-ttu-id="0bec2-104">Добавьте правила tooalert действия в службе анализа журналов</span><span class="sxs-lookup"><span data-stu-id="0bec2-104">Add actions tooalert rules in Log Analytics</span></span>
<span data-ttu-id="0bec2-105">Когда [предупреждение создается в службе анализа журналов](log-analytics-alerts.md), предусмотрена возможность hello [Настройка правила оповещения hello](log-analytics-alerts.md) tooperform одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="0bec2-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have hello option of [configuring hello alert rule](log-analytics-alerts.md) tooperform one or more actions.</span></span>  <span data-ttu-id="0bec2-106">Эта статья описывает hello различные действия, которые доступны и сведения о настройке каждого типа.</span><span class="sxs-lookup"><span data-stu-id="0bec2-106">This article describes hello different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="0bec2-107">Действие</span><span class="sxs-lookup"><span data-stu-id="0bec2-107">Action</span></span> | <span data-ttu-id="0bec2-108">Описание</span><span class="sxs-lookup"><span data-stu-id="0bec2-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="0bec2-109">Электронная почта</span><span class="sxs-lookup"><span data-stu-id="0bec2-109">Email</span></span>](#email-actions) | <span data-ttu-id="0bec2-110">Отправьте электронное письмо с подробными сведениями hello предупреждения tooone hello или нескольких получателей.</span><span class="sxs-lookup"><span data-stu-id="0bec2-110">Send an e-mail with hello details of hello alert tooone or more recipients.</span></span> |
| [<span data-ttu-id="0bec2-111">webhook</span><span class="sxs-lookup"><span data-stu-id="0bec2-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="0bec2-112">Вызов внешнего процесса с помощью одного запроса HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="0bec2-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="0bec2-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="0bec2-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="0bec2-114">Запуск модуля Runbook в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="0bec2-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="0bec2-115">Действия электронной почты</span><span class="sxs-lookup"><span data-stu-id="0bec2-115">Email actions</span></span>
<span data-ttu-id="0bec2-116">Действия по электронной почте Отправить электронное письмо с подробными сведениями hello предупреждения tooone hello или нескольких получателей.</span><span class="sxs-lookup"><span data-stu-id="0bec2-116">Email actions send an e-mail with hello details of hello alert tooone or more recipients.</span></span>  <span data-ttu-id="0bec2-117">Можно указать hello тему hello mail, но его содержимое — это стандартный формат, созданный службой аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="0bec2-117">You can specify hello subject of hello mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="0bec2-118">Он включает сводные сведения, такие как имя hello предупреждение hello в toodetails сложения из записей tooten возвращенных hello поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="0bec2-118">It includes summary information such as hello name of hello alert in addition toodetails of up tooten records returned by hello log search.</span></span>  <span data-ttu-id="0bec2-119">Она также включает поиска журнала tooa ссылку для анализа журналов, которая вернет hello полного набора записей из этого запроса.</span><span class="sxs-lookup"><span data-stu-id="0bec2-119">It also includes a link tooa log search in Log Analytics that will return hello entire set of records from that query.</span></span>   <span data-ttu-id="0bec2-120">Отправитель Hello почты hello *Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* .</span><span class="sxs-lookup"><span data-stu-id="0bec2-120">hello sender of hello mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="0bec2-121">Действия электронной почты требуют свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="0bec2-121">Email actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="0bec2-122">Свойство</span><span class="sxs-lookup"><span data-stu-id="0bec2-122">Property</span></span> | <span data-ttu-id="0bec2-123">Описание</span><span class="sxs-lookup"><span data-stu-id="0bec2-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0bec2-124">Субъект</span><span class="sxs-lookup"><span data-stu-id="0bec2-124">Subject</span></span> |<span data-ttu-id="0bec2-125">Темы в сообщении электронной почты hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-125">Subject in hello email.</span></span>  <span data-ttu-id="0bec2-126">Не удается изменить текст hello почты hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-126">You cannot modify hello body of hello mail.</span></span> |
| <span data-ttu-id="0bec2-127">Recipients</span><span class="sxs-lookup"><span data-stu-id="0bec2-127">Recipients</span></span> |<span data-ttu-id="0bec2-128">Адреса всех получателей электронной почты.</span><span class="sxs-lookup"><span data-stu-id="0bec2-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="0bec2-129">Если указать более одного адреса, а затем отдельной hello адреса точкой с запятой (;).</span><span class="sxs-lookup"><span data-stu-id="0bec2-129">If you specify more than one address, then separate hello addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="0bec2-130">Действия webhook</span><span class="sxs-lookup"><span data-stu-id="0bec2-130">Webhook actions</span></span>

<span data-ttu-id="0bec2-131">Веб-перехватчика действия позволяют проводить tooinvoke внешний процесс с помощью одного запроса HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="0bec2-131">Webhook actions allow you tooinvoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="0bec2-132">вызываемой службы Hello следует поддерживать веб-перехватчиков и определить, как использовать все полезные данные получит.</span><span class="sxs-lookup"><span data-stu-id="0bec2-132">hello service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="0bec2-133">Можно также вызвать API REST, который не поддерживает специально веб-перехватчики при условии, что запрос hello находится в формате, который понимает API hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-133">You could also call a REST API that doesn't specifically support webhooks as long as hello request is in a format that hello API understands.</span></span>  <span data-ttu-id="0bec2-134">Примеры использования веб-перехватчик в предупреждении tooan ответ отправляется сообщение [Slack](http://slack.com) или создании инцидента в [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="0bec2-134">Examples of using a webhook in response tooan alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="0bec2-135">Полное Пошаговое руководство по Создание правила оповещения с помощью веб-перехватчика toocall Slack доступен на [веб-привязок к службе анализа журналов оповещений](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="0bec2-135">A complete walkthrough of creating an alert rule with a webhook toocall Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="0bec2-136">Веб-перехватчика действия требуют свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="0bec2-136">Webhook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="0bec2-137">Свойство</span><span class="sxs-lookup"><span data-stu-id="0bec2-137">Property</span></span> | <span data-ttu-id="0bec2-138">Описание</span><span class="sxs-lookup"><span data-stu-id="0bec2-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0bec2-139">URL-адрес Webhook</span><span class="sxs-lookup"><span data-stu-id="0bec2-139">Webhook URL</span></span> |<span data-ttu-id="0bec2-140">Hello URL-адрес веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-140">hello URL of hello webhook.</span></span> |
| <span data-ttu-id="0bec2-141">Настраиваемые полезные данные JSON</span><span class="sxs-lookup"><span data-stu-id="0bec2-141">Custom JSON payload</span></span> |<span data-ttu-id="0bec2-142">Toosend настраиваемые полезные данные с веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-142">Custom payload toosend with hello webhook.</span></span>  <span data-ttu-id="0bec2-143">Дополнительные сведения см. ниже.</span><span class="sxs-lookup"><span data-stu-id="0bec2-143">See below for details.</span></span> |


<span data-ttu-id="0bec2-144">Веб-перехватчиков включают URL-адрес и полезные данные форматирования в формате JSON, hello данные отправляются toohello внешней службы.</span><span class="sxs-lookup"><span data-stu-id="0bec2-144">Webhooks include a URL and a payload formatted in JSON that is hello data sent toohello external service.</span></span>  <span data-ttu-id="0bec2-145">По умолчанию hello полезных данных будет содержать значения hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="0bec2-145">By default, hello payload will include hello values in hello following table.</span></span>  <span data-ttu-id="0bec2-146">Вы можете tooreplace эти полезные данные с новый самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="0bec2-146">You can choose tooreplace this payload with a custom one of your own.</span></span>  <span data-ttu-id="0bec2-147">В этом случае можно использовать переменные hello hello таблицы для каждого из параметров tooinclude hello их значения в настраиваемые полезные данные.</span><span class="sxs-lookup"><span data-stu-id="0bec2-147">In that case you can use hello variables in hello table for each of hello parameters tooinclude their value in your custom payload.</span></span>

| <span data-ttu-id="0bec2-148">Параметр</span><span class="sxs-lookup"><span data-stu-id="0bec2-148">Parameter</span></span> | <span data-ttu-id="0bec2-149">Переменная</span><span class="sxs-lookup"><span data-stu-id="0bec2-149">Variable</span></span> | <span data-ttu-id="0bec2-150">Описание</span><span class="sxs-lookup"><span data-stu-id="0bec2-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0bec2-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="0bec2-151">AlertRuleName</span></span> |<span data-ttu-id="0bec2-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="0bec2-152">#alertrulename</span></span> |<span data-ttu-id="0bec2-153">Имя правила оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-153">Name of hello alert rule.</span></span> |
| <span data-ttu-id="0bec2-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="0bec2-154">AlertThresholdOperator</span></span> |<span data-ttu-id="0bec2-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="0bec2-155">#thresholdoperator</span></span> |<span data-ttu-id="0bec2-156">Оператор пороговое значение для правила оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-156">Threshold operator for hello alert rule.</span></span>  <span data-ttu-id="0bec2-157">*Больше* или *Меньше*.</span><span class="sxs-lookup"><span data-stu-id="0bec2-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="0bec2-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="0bec2-158">AlertThresholdValue</span></span> |<span data-ttu-id="0bec2-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="0bec2-159">#thresholdvalue</span></span> |<span data-ttu-id="0bec2-160">Пороговое значение для правила оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-160">Threshold value for hello alert rule.</span></span> |
| <span data-ttu-id="0bec2-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="0bec2-161">LinkToSearchResults</span></span> |<span data-ttu-id="0bec2-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="0bec2-162">#linktosearchresults</span></span> |<span data-ttu-id="0bec2-163">Свяжите tooLog поиска журналов для аналитики, возвращающий hello записи из hello запрос, созданный hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="0bec2-163">Link tooLog Analytics log search that returns hello records from hello query that created hello alert.</span></span> |
| <span data-ttu-id="0bec2-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="0bec2-164">ResultCount</span></span> |<span data-ttu-id="0bec2-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="0bec2-165">#searchresultcount</span></span> |<span data-ttu-id="0bec2-166">Число записей в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-166">Number of records in hello search results.</span></span> |
| <span data-ttu-id="0bec2-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="0bec2-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="0bec2-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="0bec2-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="0bec2-169">Время окончания для hello запроса в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="0bec2-169">End time for hello query in UTC format.</span></span> |
| <span data-ttu-id="0bec2-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="0bec2-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="0bec2-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="0bec2-171">#searchinterval</span></span> |<span data-ttu-id="0bec2-172">Окно времени для правила оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-172">Time window for hello alert rule.</span></span> |
| <span data-ttu-id="0bec2-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="0bec2-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="0bec2-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="0bec2-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="0bec2-175">Время начала для hello запроса в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="0bec2-175">Start time for hello query in UTC format.</span></span> |
| <span data-ttu-id="0bec2-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="0bec2-176">SearchQuery</span></span> |<span data-ttu-id="0bec2-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="0bec2-177">#searchquery</span></span> |<span data-ttu-id="0bec2-178">Запрос поиска журнала используются правилом оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-178">Log search query used by hello alert rule.</span></span> |
| <span data-ttu-id="0bec2-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="0bec2-179">SearchResults</span></span> |<span data-ttu-id="0bec2-180">См. ниже</span><span class="sxs-lookup"><span data-stu-id="0bec2-180">See below</span></span> |<span data-ttu-id="0bec2-181">Записей, возвращаемых запросом hello в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="0bec2-181">Records returned by hello query in JSON format.</span></span>  <span data-ttu-id="0bec2-182">Ограниченная toohello первых 5 000 записей.</span><span class="sxs-lookup"><span data-stu-id="0bec2-182">Limited toohello first 5,000 records.</span></span> |
| <span data-ttu-id="0bec2-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="0bec2-183">WorkspaceID</span></span> |<span data-ttu-id="0bec2-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="0bec2-184">#workspaceid</span></span> |<span data-ttu-id="0bec2-185">Идентификатор рабочей области OMS</span><span class="sxs-lookup"><span data-stu-id="0bec2-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="0bec2-186">Например, можно указать следующие настраиваемые полезные данные, который включает один параметр с именем hello *текст*.</span><span class="sxs-lookup"><span data-stu-id="0bec2-186">For example, you might specify hello following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="0bec2-187">Этот параметр будет ожидать Hello служба, которая вызывает этот веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="0bec2-187">hello service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="0bec2-188">Этот пример полезных данных разрешится toosomething как hello при после отправки toohello веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="0bec2-188">This example payload would resolve toosomething like hello following when sent toohello webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="0bec2-189">Результаты поиска tooinclude в настраиваемые полезные данные, добавьте hello, следующей строкой как свойство верхнего уровня в полезных данных json hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-189">tooinclude search results in a custom payload, add hello following line as a top level property in hello json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="0bec2-190">Например toocreate настраиваемые полезные данные, включает только имя предупреждения hello и результаты поиска hello, можно использовать следующие hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-190">For example, toocreate a custom payload that includes just hello alert name and hello search results, you could use hello following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="0bec2-191">Вы можете выполнить полный пример создания правила оповещения с toostart веб-перехватчика внешней службы в [создания оповещений веб-перехватчика действий в tooSlack сообщения toosend аналитики журнала OMS](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="0bec2-191">You can walk through a complete example of creating an alert rule with a webhook toostart an external service at [Create an alert webhook action in OMS Log Analytics toosend message tooSlack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="0bec2-192">Действия Runbook</span><span class="sxs-lookup"><span data-stu-id="0bec2-192">Runbook actions</span></span>
<span data-ttu-id="0bec2-193">Действия Runbook запускают модуль Runbook в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="0bec2-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="0bec2-194">Чтобы toouse этот тип действий, необходимо иметь hello [решение автоматизации](log-analytics-add-solutions.md) устанавливается и настраивается в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="0bec2-194">In order toouse this type of action, you must have hello [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="0bec2-195">Можно выбрать из модулей Runbook hello в учетной записи автоматизации hello, настроенного в hello решение автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0bec2-195">You can select from hello runbooks in hello automation account that you configured in hello Automation solution.</span></span>

<span data-ttu-id="0bec2-196">Действия Runbook требуют свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="0bec2-196">Runbook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="0bec2-197">Свойство</span><span class="sxs-lookup"><span data-stu-id="0bec2-197">Property</span></span> | <span data-ttu-id="0bec2-198">Описание</span><span class="sxs-lookup"><span data-stu-id="0bec2-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="0bec2-199">Модуль Runbook</span><span class="sxs-lookup"><span data-stu-id="0bec2-199">Runbook</span></span> | <span data-ttu-id="0bec2-200">Модуль Runbook будет toostart при создании оповещения.</span><span class="sxs-lookup"><span data-stu-id="0bec2-200">Runbook that you want toostart when an alert is created.</span></span> |
| <span data-ttu-id="0bec2-201">Запуск на</span><span class="sxs-lookup"><span data-stu-id="0bec2-201">Run on</span></span> | <span data-ttu-id="0bec2-202">Укажите **Azure** toorun hello runbook в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-202">Specify **Azure** toorun hello runbook in hello cloud.</span></span>  <span data-ttu-id="0bec2-203">Укажите **гибридной рабочей роли** toorun runbook hello на агенте с [гибридной рабочей ролью Runbook](../automation/automation-hybrid-runbook-worker.md ) установлен.</span><span class="sxs-lookup"><span data-stu-id="0bec2-203">Specify **Hybrid worker** toorun hello runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="0bec2-204">Запуск действия Runbook hello runbook с помощью [веб-перехватчика](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="0bec2-204">Runbook actions start hello runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="0bec2-205">При создании правила оповещения hello, он автоматически создаст новый веб-перехватчика для hello runbook с именем hello **исправления оповещения OMS** идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="0bec2-205">When you create hello alert rule, it will automatically create a new webhook for hello runbook with hello name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="0bec2-206">Невозможно напрямую заполнить все параметры модуля runbook hello, но, hello [$WebhookData параметр](../automation/automation-webhooks.md) будет включать сведения hello hello предупреждении, включая hello результатов поиска журналов hello, в которой он был создан.</span><span class="sxs-lookup"><span data-stu-id="0bec2-206">You cannot directly populate any parameters of hello runbook, but hello [$WebhookData parameter](../automation/automation-webhooks.md) will include hello details of hello alert, including hello results of hello log search that created it.</span></span>  <span data-ttu-id="0bec2-207">Hello runbook потребуется toodefine **$WebhookData** как параметр для него tooaccess hello свойства предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-207">hello runbook will need toodefine **$WebhookData** as a parameter for it tooaccess hello properties of hello alert.</span></span>  <span data-ttu-id="0bec2-208">Hello данных предупреждений в формате json в одиночное свойство **SearchResults** в hello **RequestBody** свойство **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="0bec2-208">hello alert data is available in json format in a single property called **SearchResults** in hello **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="0bec2-209">Это окажет со свойствами hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="0bec2-209">This will have with hello properties in hello following table.</span></span>

| <span data-ttu-id="0bec2-210">Узел</span><span class="sxs-lookup"><span data-stu-id="0bec2-210">Node</span></span> | <span data-ttu-id="0bec2-211">Описание</span><span class="sxs-lookup"><span data-stu-id="0bec2-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0bec2-212">id</span><span class="sxs-lookup"><span data-stu-id="0bec2-212">id</span></span> |<span data-ttu-id="0bec2-213">Путь и идентификатор GUID для поиска hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-213">Path and GUID of hello search.</span></span> |
| <span data-ttu-id="0bec2-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="0bec2-214">__metadata</span></span> |<span data-ttu-id="0bec2-215">Сведения о hello предупреждения включая hello количество записей и состоянии hello результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="0bec2-215">Information about hello alert including hello number of records and status of hello search results.</span></span> |
| <span data-ttu-id="0bec2-216">value</span><span class="sxs-lookup"><span data-stu-id="0bec2-216">value</span></span> |<span data-ttu-id="0bec2-217">Отдельную запись для каждой записи в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-217">Separate entry for each record in hello search results.</span></span>  <span data-ttu-id="0bec2-218">Hello сведения о записи hello будет соответствовать hello свойства и значения записи hello.</span><span class="sxs-lookup"><span data-stu-id="0bec2-218">hello details of hello entry will match hello properties and values of hello record.</span></span> |

<span data-ttu-id="0bec2-219">Например hello следующие runbook следует извлечь hello записей, возвращаемых поиска журналов hello и назначить различные свойства, в зависимости от типа hello каждой записи.</span><span class="sxs-lookup"><span data-stu-id="0bec2-219">For example, hello following runbook would extract hello records returned by hello log search  and assign different properties based on hello type of each record.</span></span>  <span data-ttu-id="0bec2-220">Обратите внимание, runbook hello запускается путем преобразования **RequestBody** из json, так что он может работать как объект в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0bec2-220">Note that hello runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="0bec2-221">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0bec2-221">Next steps</span></span>
- <span data-ttu-id="0bec2-222">Вы можете выполнить пошаговое руководство по [настройке webook](log-analytics-alerts-webhooks.md) с использованием правила генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="0bec2-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="0bec2-223">Узнайте, как toowrite [Runbook в автоматизации Azure](https://azure.microsoft.com/documentation/services/automation) tooremediate проблемы определяется предупреждения.</span><span class="sxs-lookup"><span data-stu-id="0bec2-223">Learn how toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problems identified by alerts.</span></span>
