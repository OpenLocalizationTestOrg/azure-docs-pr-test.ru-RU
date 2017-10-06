---
title: "aaaSaved поиск и предупреждений в решениях OMS | Документы Microsoft"
description: "Как правило, решения в OMS включает сохраненные поисковые запросы в службе анализа журналов tooanalyze данные, собранные решением hello.  Они могут также определить предупреждения toonotify hello пользователем или автоматически выполнять определенные операции в ответ tooa критическую ошибку.  В этой статье описывается процедура toodefine анализа журналов сохранения оповещения и поиск в шаблон ARM, они могут быть включены в решения для управления."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a><span data-ttu-id="d9230-105">Добавление службы анализа журналов сохранены tooOMS оповещения и поиск решения для управления (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="d9230-105">Adding Log Analytics saved searches and alerts tooOMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="d9230-106">Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="d9230-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="d9230-107">Ни одной схеме, описанной ниже — toochange субъекта.</span><span class="sxs-lookup"><span data-stu-id="d9230-107">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="d9230-108">[Решения для управления в OMS](operations-management-suite-solutions.md) как правило, включает [сохраненные поисковые запросы](../log-analytics/log-analytics-log-searches.md) в службе анализа журналов tooanalyze данные, собранные решением hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooanalyze data collected by hello solution.</span></span>  <span data-ttu-id="d9230-109">Они также могут определять [оповещения](../log-analytics/log-analytics-alerts.md) toonotify hello пользователем или автоматически выполнять определенные операции в ответ tooa критическую ошибку.</span><span class="sxs-lookup"><span data-stu-id="d9230-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) toonotify hello user or automatically take action in response tooa critical issue.</span></span>  <span data-ttu-id="d9230-110">В этой статье описывается процедура сохранения toodefine анализа журналов, поиска и оповещений в [управление ресурсами шаблона](../resource-manager-template-walkthrough.md) , они могут быть включены в [решения для управления](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="d9230-110">This article describes how toodefine Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d9230-111">Hello примеры в этой статье с помощью параметров и переменные, которые либо обязательными или общие toomanagement решений и описано в [создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="d9230-111">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="d9230-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d9230-112">Prerequisites</span></span>
<span data-ttu-id="d9230-113">В этой статье предполагается, что вы уже знакомы с работой слишком[создать решение управления](operations-management-suite-solutions-creating.md) и структуру hello [шаблон ARM](../resource-group-authoring-templates.md) и файл решения.</span><span class="sxs-lookup"><span data-stu-id="d9230-113">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="d9230-114">Рабочая область Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d9230-114">Log Analytics Workspace</span></span>
<span data-ttu-id="d9230-115">Все ресурсы в Log Analytics размещаются в [рабочей области](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="d9230-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="d9230-116">Как описано в [OMS рабочей области и учетной записи автоматизации](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello рабочей области не включен в решение по управлению hello, но должна существовать до установки решения hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello workspace isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="d9230-117">Если эти сведения недоступны, то произойдет сбой установки решения hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-117">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="d9230-118">Имя Hello hello рабочей области находится в hello имя каждого ресурса анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="d9230-118">hello name of hello workspace is in hello name of each Log Analytics resource.</span></span>  <span data-ttu-id="d9230-119">Для этого в решении hello с hello **рабочей** параметра как следующий пример сохраненным результатом поиска ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-119">This is done in hello solution with hello **workspace** parameter as in hello following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="d9230-120">Сохраненные поиски</span><span class="sxs-lookup"><span data-stu-id="d9230-120">Saved Searches</span></span>
<span data-ttu-id="d9230-121">Включить [сохраненные поисковые запросы](../log-analytics/log-analytics-log-searches.md) в решение tooallow пользователей tooquery данные, собранные в решении.</span><span class="sxs-lookup"><span data-stu-id="d9230-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution tooallow users tooquery data collected by your solution.</span></span>  <span data-ttu-id="d9230-122">Сохраненные условия поиска будут отображаться в узле **Избранное** на портале OMS hello и **сохраненные поиски** в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d9230-122">Saved searches will appear under **Favorites** in hello OMS portal and **Saved Searches** in hello Azure portal .</span></span>  <span data-ttu-id="d9230-123">Сохраненный поиск также является обязательным для каждого оповещения.</span><span class="sxs-lookup"><span data-stu-id="d9230-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="d9230-124">[Служба аналитики журналов сохраненного поиска](../log-analytics/log-analytics-log-searches.md) ресурсы имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches` и имеют следующие структуры hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have hello following structure.</span></span>  <span data-ttu-id="d9230-125">Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



<span data-ttu-id="d9230-126">Каждое из свойств hello сохраненного поиска описаны в следующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-126">Each of hello properties of a saved search are described in hello following table.</span></span> 

| <span data-ttu-id="d9230-127">Свойство</span><span class="sxs-lookup"><span data-stu-id="d9230-127">Property</span></span> | <span data-ttu-id="d9230-128">Описание</span><span class="sxs-lookup"><span data-stu-id="d9230-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d9230-129">category</span><span class="sxs-lookup"><span data-stu-id="d9230-129">category</span></span> | <span data-ttu-id="d9230-130">Категория Hello hello сохраненные условия поиска.</span><span class="sxs-lookup"><span data-stu-id="d9230-130">hello category for hello saved search.</span></span>  <span data-ttu-id="d9230-131">Все сохраненные поисковые запросы в hello того же решения часто общей папки одной категории, они группируются в консоли hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-131">Any saved searches in hello same solution will often share a single category so they are grouped together in hello console.</span></span> |
| <span data-ttu-id="d9230-132">displayname</span><span class="sxs-lookup"><span data-stu-id="d9230-132">displayname</span></span> | <span data-ttu-id="d9230-133">Имя toodisplay для hello сохраненного поиска в портале hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-133">Name toodisplay for hello saved search in hello portal.</span></span> |
| <span data-ttu-id="d9230-134">query</span><span class="sxs-lookup"><span data-stu-id="d9230-134">query</span></span> | <span data-ttu-id="d9230-135">Toorun запроса.</span><span class="sxs-lookup"><span data-stu-id="d9230-135">Query toorun.</span></span> |

> [!NOTE]
> <span data-ttu-id="d9230-136">Toouse escape-символы в запросе hello может понадобиться, если он содержит символы, которые можно интерпретировать как JSON.</span><span class="sxs-lookup"><span data-stu-id="d9230-136">You may need toouse escape characters in hello query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="d9230-137">Например, если запрос был **OperationName:"Microsoft.Compute/virtualMachines/write типа: AzureActivity»**, должен быть записан в файл решения hello как **Имя_операции типа: AzureActivity:\" Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="d9230-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in hello solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="d9230-138">Оповещения</span><span class="sxs-lookup"><span data-stu-id="d9230-138">Alerts</span></span>
<span data-ttu-id="d9230-139">[Оповещения Log Analytics](../log-analytics/log-analytics-alerts.md) создаются правилами генерации оповещений, которые выполняют сохраненный через равные промежутки времени.</span><span class="sxs-lookup"><span data-stu-id="d9230-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="d9230-140">Если hello результаты запроса hello соответствующих указанным критериям, создается запись предупреждений и выполняются одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="d9230-140">If hello results of hello query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="d9230-141">Правила оповещений в решении для управления состоят из следующих трех разных ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-141">Alert rules in a management solution are made up of hello following three different resources.</span></span>

- <span data-ttu-id="d9230-142">**Сохраненный поиск.**</span><span class="sxs-lookup"><span data-stu-id="d9230-142">**Saved search.**</span></span>  <span data-ttu-id="d9230-143">Определяет hello поиска журналов, которые будут запущены.</span><span class="sxs-lookup"><span data-stu-id="d9230-143">Defines hello log search that will be run.</span></span>  <span data-ttu-id="d9230-144">Один сохраненный поиск может использоваться несколькими правилами генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="d9230-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="d9230-145">**Расписание.**</span><span class="sxs-lookup"><span data-stu-id="d9230-145">**Schedule.**</span></span>  <span data-ttu-id="d9230-146">Определяет, как часто hello поиска журналов будет выполняться.</span><span class="sxs-lookup"><span data-stu-id="d9230-146">Defines how often hello log search will be run.</span></span>  <span data-ttu-id="d9230-147">У каждого правила генерации оповещений будет только одно расписание.</span><span class="sxs-lookup"><span data-stu-id="d9230-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="d9230-148">**Действие оповещения.**</span><span class="sxs-lookup"><span data-stu-id="d9230-148">**Alert action.**</span></span>  <span data-ttu-id="d9230-149">Каждое правило оповещения будут иметь один ресурс действие с типом **предупреждение** , определяющий hello подробные сведения о предупреждении hello, например hello критерий будет создана запись предупреждений и hello серьезность предупреждения.</span><span class="sxs-lookup"><span data-stu-id="d9230-149">Each alert rule will have one action resource with a type of **Alert** that defines hello details of hello alert such as hello criteria for when an alert record will be created and hello alert's severity.</span></span>  <span data-ttu-id="d9230-150">ресурс действие Hello будет определять ответ почты и runbook.</span><span class="sxs-lookup"><span data-stu-id="d9230-150">hello action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="d9230-151">**Действие webhook (необязательно).**</span><span class="sxs-lookup"><span data-stu-id="d9230-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="d9230-152">Если правило оповещения hello будет вызывать веб-перехватчика, то требуется дополнительное действие ресурс с типом **веб-перехватчика**.</span><span class="sxs-lookup"><span data-stu-id="d9230-152">If hello alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="d9230-153">Ресурсы сохраненных поисков описаны выше.</span><span class="sxs-lookup"><span data-stu-id="d9230-153">Saved search resources are described above.</span></span>  <span data-ttu-id="d9230-154">Hello другие ресурсы, описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="d9230-154">hello other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="d9230-155">Ресурс расписания</span><span class="sxs-lookup"><span data-stu-id="d9230-155">Schedule resource</span></span>

<span data-ttu-id="d9230-156">У сохраненного поиска может быть одно или несколько расписаний, представляющих отдельное правило генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="d9230-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="d9230-157">Hello расписание определяет частоту hello поиска выполняется и hello интервал времени, через какие hello извлекаются данные.</span><span class="sxs-lookup"><span data-stu-id="d9230-157">hello schedule defines how often hello search is run and hello time interval over which hello data is retrieved.</span></span>  <span data-ttu-id="d9230-158">Планирование ресурсов имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` и имеют следующие структуры hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have hello following structure.</span></span> <span data-ttu-id="d9230-159">Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



<span data-ttu-id="d9230-160">в hello в следующей таблице описаны свойства Hello планирование ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d9230-160">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="d9230-161">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="d9230-161">Element name</span></span> | <span data-ttu-id="d9230-162">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9230-162">Required</span></span> | <span data-ttu-id="d9230-163">Описание</span><span class="sxs-lookup"><span data-stu-id="d9230-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="d9230-164">Включено</span><span class="sxs-lookup"><span data-stu-id="d9230-164">enabled</span></span>       | <span data-ttu-id="d9230-165">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-165">Yes</span></span> | <span data-ttu-id="d9230-166">Указывает, включено ли предупреждение hello при его создании.</span><span class="sxs-lookup"><span data-stu-id="d9230-166">Specifies whether hello alert is enabled when it's created.</span></span> |
| <span data-ttu-id="d9230-167">interval</span><span class="sxs-lookup"><span data-stu-id="d9230-167">interval</span></span>      | <span data-ttu-id="d9230-168">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-168">Yes</span></span> | <span data-ttu-id="d9230-169">Как часто hello запрос выполняется в минутах.</span><span class="sxs-lookup"><span data-stu-id="d9230-169">How often hello query runs in minutes.</span></span> |
| <span data-ttu-id="d9230-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="d9230-170">queryTimeSpan</span></span> | <span data-ttu-id="d9230-171">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-171">Yes</span></span> | <span data-ttu-id="d9230-172">Продолжительность времени в минутах, по которому tooevaluate результаты.</span><span class="sxs-lookup"><span data-stu-id="d9230-172">Length of time in minutes over which tooevaluate results.</span></span> |

<span data-ttu-id="d9230-173">Планирование ресурсов Hello должны зависеть от сохраненного поиска, чтобы он создан, прежде чем расписание hello hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-173">hello schedule resource should depend on hello saved search so that it's created before hello schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="d9230-174">Действия</span><span class="sxs-lookup"><span data-stu-id="d9230-174">Actions</span></span>
<span data-ttu-id="d9230-175">Существует два типа действия ресурса, указанного в hello **тип** свойства.</span><span class="sxs-lookup"><span data-stu-id="d9230-175">There are two types of action resource specified by hello **Type** property.</span></span>  <span data-ttu-id="d9230-176">Расписание требуется один **предупреждение** действия, который определяет сведения hello правило генерации оповещений hello и действия, предпринимаемые при создании оповещения.</span><span class="sxs-lookup"><span data-stu-id="d9230-176">A schedule requires one **Alert** action which defines hello details of hello alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="d9230-177">Он также может включать **веб-перехватчика** действие, если веб-перехватчика должна вызываться из hello предупреждения.</span><span class="sxs-lookup"><span data-stu-id="d9230-177">It may also include a **Webhook** action if a webhook should be called from hello alert.</span></span>  

<span data-ttu-id="d9230-178">Ресурсы действия имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="d9230-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="d9230-179">Действия оповещений</span><span class="sxs-lookup"><span data-stu-id="d9230-179">Alert actions</span></span>

<span data-ttu-id="d9230-180">У каждого расписания будет одно действие **Alert**.</span><span class="sxs-lookup"><span data-stu-id="d9230-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="d9230-181">Определяет сведения hello hello предупреждение, и при необходимости действия уведомления и исправления.</span><span class="sxs-lookup"><span data-stu-id="d9230-181">This defines hello details of hello alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="d9230-182">Уведомление отправляется по электронной почте tooone или несколько адресов.</span><span class="sxs-lookup"><span data-stu-id="d9230-182">A notification sends an email tooone or more addresses.</span></span>  <span data-ttu-id="d9230-183">Исправление запуск модуля runbook в автоматизации Azure tooattempt tooremediate hello обнаружена проблема.</span><span class="sxs-lookup"><span data-stu-id="d9230-183">A remediation starts a runbook in Azure Automation tooattempt tooremediate hello detected issue.</span></span>

<span data-ttu-id="d9230-184">Оповещения имеют следующие структуры hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-184">Alert actions have hello following structure.</span></span>  <span data-ttu-id="d9230-185">Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

<span data-ttu-id="d9230-186">свойства Hello ресурсов действие предупреждения описаны в следующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-186">hello properties for Alert action resources are described in hello following tables.</span></span>

| <span data-ttu-id="d9230-187">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="d9230-187">Element name</span></span> | <span data-ttu-id="d9230-188">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9230-188">Required</span></span> | <span data-ttu-id="d9230-189">Описание</span><span class="sxs-lookup"><span data-stu-id="d9230-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="d9230-190">Тип</span><span class="sxs-lookup"><span data-stu-id="d9230-190">Type</span></span> | <span data-ttu-id="d9230-191">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-191">Yes</span></span> | <span data-ttu-id="d9230-192">Тип действия hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-192">Type of hello action.</span></span>  <span data-ttu-id="d9230-193">Для действий оповещения это будет **Alert**.</span><span class="sxs-lookup"><span data-stu-id="d9230-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="d9230-194">Имя</span><span class="sxs-lookup"><span data-stu-id="d9230-194">Name</span></span> | <span data-ttu-id="d9230-195">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-195">Yes</span></span> | <span data-ttu-id="d9230-196">Отображаемое имя для hello предупреждения.</span><span class="sxs-lookup"><span data-stu-id="d9230-196">Display name for hello alert.</span></span>  <span data-ttu-id="d9230-197">Это имя hello, которое отображается в консоли hello для правила оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-197">This is hello name that's displayed in hello console for hello alert rule.</span></span> |
| <span data-ttu-id="d9230-198">Описание</span><span class="sxs-lookup"><span data-stu-id="d9230-198">Description</span></span> | <span data-ttu-id="d9230-199">Нет</span><span class="sxs-lookup"><span data-stu-id="d9230-199">No</span></span> | <span data-ttu-id="d9230-200">Необязательное описание предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-200">Optional description of hello alert.</span></span> |
| <span data-ttu-id="d9230-201">Severity</span><span class="sxs-lookup"><span data-stu-id="d9230-201">Severity</span></span> | <span data-ttu-id="d9230-202">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-202">Yes</span></span> | <span data-ttu-id="d9230-203">Серьезность предупреждения записи hello из hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="d9230-203">Severity of hello alert record from hello following values:</span></span><br><br> <span data-ttu-id="d9230-204">**Critical**</span><span class="sxs-lookup"><span data-stu-id="d9230-204">**Critical**</span></span><br><span data-ttu-id="d9230-205">**Предупреждение;**</span><span class="sxs-lookup"><span data-stu-id="d9230-205">**Warning**</span></span><br><span data-ttu-id="d9230-206">**Informational**</span><span class="sxs-lookup"><span data-stu-id="d9230-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="d9230-207">Threshold (Пороговое значение)</span><span class="sxs-lookup"><span data-stu-id="d9230-207">Threshold</span></span>
<span data-ttu-id="d9230-208">Это обязательный раздел.</span><span class="sxs-lookup"><span data-stu-id="d9230-208">This section is required.</span></span>  <span data-ttu-id="d9230-209">Он определяет свойства hello hello порога оповещения.</span><span class="sxs-lookup"><span data-stu-id="d9230-209">It defines hello properties for hello alert threshold.</span></span>

| <span data-ttu-id="d9230-210">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="d9230-210">Element name</span></span> | <span data-ttu-id="d9230-211">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9230-211">Required</span></span> | <span data-ttu-id="d9230-212">Описание</span><span class="sxs-lookup"><span data-stu-id="d9230-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="d9230-213">Оператор</span><span class="sxs-lookup"><span data-stu-id="d9230-213">Operator</span></span> | <span data-ttu-id="d9230-214">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-214">Yes</span></span> | <span data-ttu-id="d9230-215">Оператор для сравнения hello из hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="d9230-215">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="d9230-216">**gt — больше;<br>lt — меньше.**</span><span class="sxs-lookup"><span data-stu-id="d9230-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="d9230-217">Значение</span><span class="sxs-lookup"><span data-stu-id="d9230-217">Value</span></span> | <span data-ttu-id="d9230-218">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-218">Yes</span></span> | <span data-ttu-id="d9230-219">результаты hello toocompare значение Hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-219">hello value toocompare hello results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="d9230-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="d9230-220">MetricsTrigger</span></span>
<span data-ttu-id="d9230-221">Это необязательный раздел.</span><span class="sxs-lookup"><span data-stu-id="d9230-221">This section is optional.</span></span>  <span data-ttu-id="d9230-222">Он добавляется для оповещения об измерении метрики.</span><span class="sxs-lookup"><span data-stu-id="d9230-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="d9230-223">Оповещения об измерении метрики в настоящее время находятся на этапе общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="d9230-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="d9230-224">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="d9230-224">Element name</span></span> | <span data-ttu-id="d9230-225">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9230-225">Required</span></span> | <span data-ttu-id="d9230-226">Описание</span><span class="sxs-lookup"><span data-stu-id="d9230-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="d9230-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="d9230-227">TriggerCondition</span></span> | <span data-ttu-id="d9230-228">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-228">Yes</span></span> | <span data-ttu-id="d9230-229">Указывает, является ли hello пороговое значение для общее число нарушений или последовательных нарушения безопасности hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="d9230-229">Specifies whether hello threshold is for total number of breaches or consecutive breaches from hello following values:</span></span><br><br><span data-ttu-id="d9230-230">**Total;<br>Consecutive.**</span><span class="sxs-lookup"><span data-stu-id="d9230-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="d9230-231">Оператор</span><span class="sxs-lookup"><span data-stu-id="d9230-231">Operator</span></span> | <span data-ttu-id="d9230-232">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-232">Yes</span></span> | <span data-ttu-id="d9230-233">Оператор для сравнения hello из hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="d9230-233">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="d9230-234">**gt — больше;<br>lt — меньше.**</span><span class="sxs-lookup"><span data-stu-id="d9230-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="d9230-235">Значение</span><span class="sxs-lookup"><span data-stu-id="d9230-235">Value</span></span> | <span data-ttu-id="d9230-236">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-236">Yes</span></span> | <span data-ttu-id="d9230-237">Число hello время hello условия должно быть выполнены tootrigger hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="d9230-237">Number of hello times hello criteria must be met tootrigger hello alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="d9230-238">Регулирование</span><span class="sxs-lookup"><span data-stu-id="d9230-238">Throttling</span></span>
<span data-ttu-id="d9230-239">Это необязательный раздел.</span><span class="sxs-lookup"><span data-stu-id="d9230-239">This section is optional.</span></span>  <span data-ttu-id="d9230-240">Включите в этом разделе, если требуется, чтобы предупреждения toosuppress от hello же правило минимальное количество времени, после создания предупреждения.</span><span class="sxs-lookup"><span data-stu-id="d9230-240">Include this section if you want toosuppress alerts from hello same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="d9230-241">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="d9230-241">Element name</span></span> | <span data-ttu-id="d9230-242">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9230-242">Required</span></span> | <span data-ttu-id="d9230-243">Описание</span><span class="sxs-lookup"><span data-stu-id="d9230-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="d9230-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="d9230-244">DurationInMinutes</span></span> | <span data-ttu-id="d9230-245">Значение Yes, если добавлен элемент Throttling.</span><span class="sxs-lookup"><span data-stu-id="d9230-245">Yes if Throttling element included</span></span> | <span data-ttu-id="d9230-246">Число минут toosuppress оповещений после одного из hello созданных же правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="d9230-246">Number of minutes toosuppress alerts after one from hello same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="d9230-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="d9230-247">EmailNotification</span></span>
 <span data-ttu-id="d9230-248">Этот раздел является необязательным включить его, если вы хотите hello предупреждения toosend mail tooone или нескольких получателей.</span><span class="sxs-lookup"><span data-stu-id="d9230-248">This section is optional  Include it if you want hello alert toosend mail tooone or more recipients.</span></span>

| <span data-ttu-id="d9230-249">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="d9230-249">Element name</span></span> | <span data-ttu-id="d9230-250">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9230-250">Required</span></span> | <span data-ttu-id="d9230-251">Описание</span><span class="sxs-lookup"><span data-stu-id="d9230-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="d9230-252">Recipients</span><span class="sxs-lookup"><span data-stu-id="d9230-252">Recipients</span></span> | <span data-ttu-id="d9230-253">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-253">Yes</span></span> | <span data-ttu-id="d9230-254">Список с разделителями-запятыми по электронной почте адресов toosend уведомление при создании оповещения как в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-254">Comma delimited list of email addresses toosend notification when an alert is created such as in hello following example.</span></span><br><br><span data-ttu-id="d9230-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="d9230-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="d9230-256">Субъект</span><span class="sxs-lookup"><span data-stu-id="d9230-256">Subject</span></span> | <span data-ttu-id="d9230-257">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-257">Yes</span></span> | <span data-ttu-id="d9230-258">Тема сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-258">Subject line of hello mail.</span></span> |
| <span data-ttu-id="d9230-259">Вложение</span><span class="sxs-lookup"><span data-stu-id="d9230-259">Attachment</span></span> | <span data-ttu-id="d9230-260">Нет</span><span class="sxs-lookup"><span data-stu-id="d9230-260">No</span></span> | <span data-ttu-id="d9230-261">Вложения в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="d9230-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="d9230-262">Если этот элемент добавлен, он должен иметь значение **None**.</span><span class="sxs-lookup"><span data-stu-id="d9230-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="d9230-263">Исправление</span><span class="sxs-lookup"><span data-stu-id="d9230-263">Remediation</span></span>
<span data-ttu-id="d9230-264">Этот раздел является необязательным включите его, если требуется, чтобы toostart runbook в предупреждении toohello ответа.</span><span class="sxs-lookup"><span data-stu-id="d9230-264">This section is optional  Include it if you want a runbook toostart in response toohello alert.</span></span> |

| <span data-ttu-id="d9230-265">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="d9230-265">Element name</span></span> | <span data-ttu-id="d9230-266">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9230-266">Required</span></span> | <span data-ttu-id="d9230-267">Описание</span><span class="sxs-lookup"><span data-stu-id="d9230-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="d9230-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="d9230-268">RunbookName</span></span> | <span data-ttu-id="d9230-269">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-269">Yes</span></span> | <span data-ttu-id="d9230-270">Имя hello runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="d9230-270">Name of hello runbook toostart.</span></span> |
| <span data-ttu-id="d9230-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="d9230-271">WebhookUri</span></span> | <span data-ttu-id="d9230-272">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-272">Yes</span></span> | <span data-ttu-id="d9230-273">URI веб-перехватчика hello для hello runbook.</span><span class="sxs-lookup"><span data-stu-id="d9230-273">Uri of hello webhook for hello runbook.</span></span> |
| <span data-ttu-id="d9230-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="d9230-274">Expiry</span></span> | <span data-ttu-id="d9230-275">Нет</span><span class="sxs-lookup"><span data-stu-id="d9230-275">No</span></span> | <span data-ttu-id="d9230-276">Дата и время hello исправления истечения срока действия.</span><span class="sxs-lookup"><span data-stu-id="d9230-276">Date and time that hello remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="d9230-277">Действия webhook</span><span class="sxs-lookup"><span data-stu-id="d9230-277">Webhook actions</span></span>

<span data-ttu-id="d9230-278">Действия веб-перехватчика запустить процесс путем вызова URL-адрес и Дополнительно может предоставлять полезные данные toobe отправлено.</span><span class="sxs-lookup"><span data-stu-id="d9230-278">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span> <span data-ttu-id="d9230-279">Они являются подобные действия tooRemediation, за исключением того, они предназначены для веб-перехватчиков, который может вызывать процессами, отличными от Runbook автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="d9230-279">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="d9230-280">Они также предоставляют hello дополнительную возможность предоставления удаленных процессов toohello toobe доставляется полезных данных.</span><span class="sxs-lookup"><span data-stu-id="d9230-280">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="d9230-281">Если оповещение будет вызывать веб-перехватчика, то он должен быть ресурс действие с типом **веб-перехватчика** в дополнение toohello **предупреждение** действия ресурса.</span><span class="sxs-lookup"><span data-stu-id="d9230-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition toohello **Alert** action resource.</span></span>  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

<span data-ttu-id="d9230-282">Hello свойств ресурсов веб-перехватчика действия описаны в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="d9230-282">hello properties for Webhook action resources are described in hello following tables.</span></span>

| <span data-ttu-id="d9230-283">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="d9230-283">Element name</span></span> | <span data-ttu-id="d9230-284">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9230-284">Required</span></span> | <span data-ttu-id="d9230-285">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="d9230-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="d9230-286">type</span><span class="sxs-lookup"><span data-stu-id="d9230-286">type</span></span> | <span data-ttu-id="d9230-287">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-287">Yes</span></span> | <span data-ttu-id="d9230-288">Тип действия hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-288">Type of hello action.</span></span>  <span data-ttu-id="d9230-289">Для действий webhook это будет **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="d9230-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="d9230-290">name</span><span class="sxs-lookup"><span data-stu-id="d9230-290">name</span></span> | <span data-ttu-id="d9230-291">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-291">Yes</span></span> | <span data-ttu-id="d9230-292">Отображаемое имя для действия hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-292">Display name for hello action.</span></span>  <span data-ttu-id="d9230-293">Не отображается в консоли hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-293">This is not displayed in hello console.</span></span> |
| <span data-ttu-id="d9230-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="d9230-294">wehookUri</span></span> | <span data-ttu-id="d9230-295">Да</span><span class="sxs-lookup"><span data-stu-id="d9230-295">Yes</span></span> | <span data-ttu-id="d9230-296">URI для веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-296">Uri for hello webhook.</span></span> |
| <span data-ttu-id="d9230-297">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="d9230-297">customPayload</span></span> | <span data-ttu-id="d9230-298">Нет</span><span class="sxs-lookup"><span data-stu-id="d9230-298">No</span></span> | <span data-ttu-id="d9230-299">Настраиваемые полезные данные отправлены toobe toohello веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="d9230-299">Custom payload toobe sent toohello webhook.</span></span> <span data-ttu-id="d9230-300">Формат Hello будет зависеть от ожидается какой веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="d9230-300">hello format will depend on what hello webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="d9230-301">Образец</span><span class="sxs-lookup"><span data-stu-id="d9230-301">Sample</span></span>

<span data-ttu-id="d9230-302">Ниже приведен образец, включают решение, включающее hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="d9230-302">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="d9230-303">Сохраненный поиск</span><span class="sxs-lookup"><span data-stu-id="d9230-303">Saved search</span></span>
- <span data-ttu-id="d9230-304">Расписание</span><span class="sxs-lookup"><span data-stu-id="d9230-304">Schedule</span></span>
- <span data-ttu-id="d9230-305">Действие оповещения</span><span class="sxs-lookup"><span data-stu-id="d9230-305">Alert action</span></span>
- <span data-ttu-id="d9230-306">Действия webhook</span><span class="sxs-lookup"><span data-stu-id="d9230-306">Webhook action</span></span>

<span data-ttu-id="d9230-307">Здравствуйте, образец использует [параметры стандартное решение](operations-management-suite-solutions-solution-file.md#parameters) переменные, которые часто используются в решении, что отличие от значений toohardcoding в hello определения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d9230-307">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


<span data-ttu-id="d9230-308">Следующий файл параметров Hello предоставляет значения, образцы для этого решения.</span><span class="sxs-lookup"><span data-stu-id="d9230-308">hello following parameter file provides samples values for this solution.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="d9230-309">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9230-309">Next steps</span></span>
* <span data-ttu-id="d9230-310">[Добавление представления](operations-management-suite-solutions-resources-views.md) tooyour решение для управления.</span><span class="sxs-lookup"><span data-stu-id="d9230-310">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="d9230-311">[Добавить Runbook автоматизации и другим ресурсам](operations-management-suite-solutions-resources-automation.md) tooyour решение для управления.</span><span class="sxs-lookup"><span data-stu-id="d9230-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>

