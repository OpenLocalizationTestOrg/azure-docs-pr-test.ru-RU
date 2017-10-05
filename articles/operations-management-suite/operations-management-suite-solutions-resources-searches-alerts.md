---
title: "Сохраненные поиски и оповещения в решениях OMS | Документация Майкрософт"
description: "Как правило, решения в OMS включают в себя возможность сохранения поисков в Log Analytics для анализа данных, собранных решением.  Они могут также определить оповещения для уведомления пользователя или автоматического выполнения действия в ответ на критическую ошибку.  В этой статье описывается, как определить сохраненные поиски и оповещения Log Analytics в шаблоне ARM, чтобы их можно было добавлять в решения для управления."
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
ms.openlocfilehash: 21c42a747a08c5386c65d10190baf0054a7adef8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-oms-management-solution-preview"></a><span data-ttu-id="c6457-105">Добавление сохраненных поисковых запросов и оповещений Log Analytics в решении по управлению OMS (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="c6457-105">Adding Log Analytics saved searches and alerts to OMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="c6457-106">Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="c6457-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="c6457-107">Любые схемы, приведенные ниже, могут измениться.</span><span class="sxs-lookup"><span data-stu-id="c6457-107">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="c6457-108">Как правило, [решения для управления в OMS](operations-management-suite-solutions.md) включают в себя возможность [сохранения поисков](../log-analytics/log-analytics-log-searches.md) в Log Analytics для анализа данных, собранных решением.</span><span class="sxs-lookup"><span data-stu-id="c6457-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span></span>  <span data-ttu-id="c6457-109">Они могут также определять [оповещения](../log-analytics/log-analytics-alerts.md) для уведомления пользователя или автоматического выполнения действия в ответ на критическую ошибку.</span><span class="sxs-lookup"><span data-stu-id="c6457-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span></span>  <span data-ttu-id="c6457-110">В этой статье описывается, как определить сохраненные поиски и оповещения Log Analytics в [шаблоне Resource Manager](../resource-manager-template-walkthrough.md), чтобы их можно было добавлять в [решения для управления](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="c6457-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c6457-111">В примерах здесь используются обязательные или общие параметры и переменные для решений по управлению, описанные в статье [Создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="c6457-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="c6457-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c6457-112">Prerequisites</span></span>
<span data-ttu-id="c6457-113">В этой статье предполагается, что вы уже знаете, как [создать решение для управления](operations-management-suite-solutions-creating.md), структуру [шаблона ARM](../resource-group-authoring-templates.md) и файл решения.</span><span class="sxs-lookup"><span data-stu-id="c6457-113">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="c6457-114">Рабочая область Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c6457-114">Log Analytics Workspace</span></span>
<span data-ttu-id="c6457-115">Все ресурсы в Log Analytics размещаются в [рабочей области](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="c6457-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="c6457-116">Как описано в разделе [Рабочая область OMS и учетная запись службы автоматизации](operations-management-suite-solutions.md#oms-workspace-and-automation-account), рабочая область не включена в решение для управления и должна быть создана до его установки.</span><span class="sxs-lookup"><span data-stu-id="c6457-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the workspace isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="c6457-117">Если она недоступна, произойдет сбой установки решения.</span><span class="sxs-lookup"><span data-stu-id="c6457-117">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="c6457-118">Имя рабочей области указывается в имени каждого ресурса Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6457-118">The name of the workspace is in the name of each Log Analytics resource.</span></span>  <span data-ttu-id="c6457-119">Для этого в решении используется параметр **workspace**, как показано в следующем примере ресурса savedsearch.</span><span class="sxs-lookup"><span data-stu-id="c6457-119">This is done in the solution with the **workspace** parameter as in the following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="c6457-120">Сохраненные поиски</span><span class="sxs-lookup"><span data-stu-id="c6457-120">Saved Searches</span></span>
<span data-ttu-id="c6457-121">Добавьте в решение функцию [сохраненных поисков](../log-analytics/log-analytics-log-searches.md), чтобы пользователи могли запрашивать данные, собранные решением.</span><span class="sxs-lookup"><span data-stu-id="c6457-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span></span>  <span data-ttu-id="c6457-122">Сохраненные поиски будут отображены в разделе **Избранное** на портале OMS и в разделе **Сохраненные условия поиска** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c6457-122">Saved searches will appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal .</span></span>  <span data-ttu-id="c6457-123">Сохраненный поиск также является обязательным для каждого оповещения.</span><span class="sxs-lookup"><span data-stu-id="c6457-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="c6457-124">Ресурсы [сохраненных поисков Log Analytics](../log-analytics/log-analytics-log-searches.md) имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches`. Их структура приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="c6457-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span></span>  <span data-ttu-id="c6457-125">Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров.</span><span class="sxs-lookup"><span data-stu-id="c6457-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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



<span data-ttu-id="c6457-126">Каждое из свойств сохраненного поиска описано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="c6457-126">Each of the properties of a saved search are described in the following table.</span></span> 

| <span data-ttu-id="c6457-127">Свойство</span><span class="sxs-lookup"><span data-stu-id="c6457-127">Property</span></span> | <span data-ttu-id="c6457-128">Описание</span><span class="sxs-lookup"><span data-stu-id="c6457-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c6457-129">category</span><span class="sxs-lookup"><span data-stu-id="c6457-129">category</span></span> | <span data-ttu-id="c6457-130">Категория для сохраненного поиска.</span><span class="sxs-lookup"><span data-stu-id="c6457-130">The category for the saved search.</span></span>  <span data-ttu-id="c6457-131">Сохраненные поиски в одном решении часто будут принадлежать одной категории, поэтому они группируются в консоли.</span><span class="sxs-lookup"><span data-stu-id="c6457-131">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span></span> |
| <span data-ttu-id="c6457-132">displayname</span><span class="sxs-lookup"><span data-stu-id="c6457-132">displayname</span></span> | <span data-ttu-id="c6457-133">Имя, отображаемое для сохраненного поиска на портале.</span><span class="sxs-lookup"><span data-stu-id="c6457-133">Name to display for the saved search in the portal.</span></span> |
| <span data-ttu-id="c6457-134">запрос</span><span class="sxs-lookup"><span data-stu-id="c6457-134">query</span></span> | <span data-ttu-id="c6457-135">Запрос для выполнения.</span><span class="sxs-lookup"><span data-stu-id="c6457-135">Query to run.</span></span> |

> [!NOTE]
> <span data-ttu-id="c6457-136">В запросе необходимо использовать escape-символы, если он содержит знаки, которые можно интерпретировать как JSON.</span><span class="sxs-lookup"><span data-stu-id="c6457-136">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="c6457-137">Например, запрос **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"** в файл решения должен быть записан как **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="c6457-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="c6457-138">Оповещения</span><span class="sxs-lookup"><span data-stu-id="c6457-138">Alerts</span></span>
<span data-ttu-id="c6457-139">[Оповещения Log Analytics](../log-analytics/log-analytics-alerts.md) создаются правилами генерации оповещений, которые выполняют сохраненный через равные промежутки времени.</span><span class="sxs-lookup"><span data-stu-id="c6457-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="c6457-140">Если результаты запроса соответствуют указанным условиям, то создается запись оповещения и выполняются одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="c6457-140">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="c6457-141">Правила генерации оповещений в решении для управления состоят из трех различных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c6457-141">Alert rules in a management solution are made up of the following three different resources.</span></span>

- <span data-ttu-id="c6457-142">**Сохраненный поиск.**</span><span class="sxs-lookup"><span data-stu-id="c6457-142">**Saved search.**</span></span>  <span data-ttu-id="c6457-143">Определяет выполняемый поиск в журнале.</span><span class="sxs-lookup"><span data-stu-id="c6457-143">Defines the log search that will be run.</span></span>  <span data-ttu-id="c6457-144">Один сохраненный поиск может использоваться несколькими правилами генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="c6457-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="c6457-145">**Расписание.**</span><span class="sxs-lookup"><span data-stu-id="c6457-145">**Schedule.**</span></span>  <span data-ttu-id="c6457-146">Определяет, как часто будет выполняться поиск в журнале.</span><span class="sxs-lookup"><span data-stu-id="c6457-146">Defines how often the log search will be run.</span></span>  <span data-ttu-id="c6457-147">У каждого правила генерации оповещений будет только одно расписание.</span><span class="sxs-lookup"><span data-stu-id="c6457-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="c6457-148">**Действие оповещения.**</span><span class="sxs-lookup"><span data-stu-id="c6457-148">**Alert action.**</span></span>  <span data-ttu-id="c6457-149">У каждого правила генерации оповещений будет один ресурс действия типа **Alert**, определяющий данные оповещения, такие как условия создания записи оповещения и серьезность оповещения.</span><span class="sxs-lookup"><span data-stu-id="c6457-149">Each alert rule will have one action resource with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record will be created and the alert's severity.</span></span>  <span data-ttu-id="c6457-150">Ресурс действия может также определять электронную почту и Runbook для ответа.</span><span class="sxs-lookup"><span data-stu-id="c6457-150">The action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="c6457-151">**Действие webhook (необязательно).**</span><span class="sxs-lookup"><span data-stu-id="c6457-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="c6457-152">Если правило генерации оповещений будет вызывать webhook, то ему требуется дополнительный ресурс действия типа **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="c6457-152">If the alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="c6457-153">Ресурсы сохраненных поисков описаны выше.</span><span class="sxs-lookup"><span data-stu-id="c6457-153">Saved search resources are described above.</span></span>  <span data-ttu-id="c6457-154">Другие ресурсы описываются ниже.</span><span class="sxs-lookup"><span data-stu-id="c6457-154">The other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="c6457-155">Ресурс расписания</span><span class="sxs-lookup"><span data-stu-id="c6457-155">Schedule resource</span></span>

<span data-ttu-id="c6457-156">У сохраненного поиска может быть одно или несколько расписаний, представляющих отдельное правило генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="c6457-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="c6457-157">Расписание определяет, как часто выполняется поиск, а также интервал времени для извлечения данных.</span><span class="sxs-lookup"><span data-stu-id="c6457-157">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span></span>  <span data-ttu-id="c6457-158">Ресурсы расписания имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/`. Их структура приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="c6457-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span></span> <span data-ttu-id="c6457-159">Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров.</span><span class="sxs-lookup"><span data-stu-id="c6457-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


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



<span data-ttu-id="c6457-160">В следующей таблице описаны свойства ресурсов расписания.</span><span class="sxs-lookup"><span data-stu-id="c6457-160">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="c6457-161">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c6457-161">Element name</span></span> | <span data-ttu-id="c6457-162">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c6457-162">Required</span></span> | <span data-ttu-id="c6457-163">Описание</span><span class="sxs-lookup"><span data-stu-id="c6457-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="c6457-164">Включено</span><span class="sxs-lookup"><span data-stu-id="c6457-164">enabled</span></span>       | <span data-ttu-id="c6457-165">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-165">Yes</span></span> | <span data-ttu-id="c6457-166">Указывает, включено ли оповещение при его создании.</span><span class="sxs-lookup"><span data-stu-id="c6457-166">Specifies whether the alert is enabled when it's created.</span></span> |
| <span data-ttu-id="c6457-167">interval</span><span class="sxs-lookup"><span data-stu-id="c6457-167">interval</span></span>      | <span data-ttu-id="c6457-168">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-168">Yes</span></span> | <span data-ttu-id="c6457-169">Как часто выполняется запрос (в минутах).</span><span class="sxs-lookup"><span data-stu-id="c6457-169">How often the query runs in minutes.</span></span> |
| <span data-ttu-id="c6457-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="c6457-170">queryTimeSpan</span></span> | <span data-ttu-id="c6457-171">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-171">Yes</span></span> | <span data-ttu-id="c6457-172">Интервал времени в минутах, на котором следует оценивать результаты.</span><span class="sxs-lookup"><span data-stu-id="c6457-172">Length of time in minutes over which to evaluate results.</span></span> |

<span data-ttu-id="c6457-173">Ресурс расписания будет зависеть от сохраненного поиска, поэтому он должен быть создан перед расписанием.</span><span class="sxs-lookup"><span data-stu-id="c6457-173">The schedule resource should depend on the saved search so that it's created before the schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="c6457-174">Действия</span><span class="sxs-lookup"><span data-stu-id="c6457-174">Actions</span></span>
<span data-ttu-id="c6457-175">Существуют два типа ресурса действия, которые задает свойство **Type**.</span><span class="sxs-lookup"><span data-stu-id="c6457-175">There are two types of action resource specified by the **Type** property.</span></span>  <span data-ttu-id="c6457-176">Для расписания требуется одно действие **Alert**, которое определяет сведения о правиле генерации оповещений и действия, предпринимаемые при создании оповещения.</span><span class="sxs-lookup"><span data-stu-id="c6457-176">A schedule requires one **Alert** action which defines the details of the alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="c6457-177">Оно может также включать в себя действие **Webhook**, если оповещение должно вызывать webhook.</span><span class="sxs-lookup"><span data-stu-id="c6457-177">It may also include a **Webhook** action if a webhook should be called from the alert.</span></span>  

<span data-ttu-id="c6457-178">Ресурсы действия имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="c6457-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="c6457-179">Действия оповещений</span><span class="sxs-lookup"><span data-stu-id="c6457-179">Alert actions</span></span>

<span data-ttu-id="c6457-180">У каждого расписания будет одно действие **Alert**.</span><span class="sxs-lookup"><span data-stu-id="c6457-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="c6457-181">Оно определяет данные оповещения и, при необходимости, уведомление и действия для исправления</span><span class="sxs-lookup"><span data-stu-id="c6457-181">This defines the details of the alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="c6457-182">Уведомление позволяет отправить электронное сообщение на один или несколько адресов.</span><span class="sxs-lookup"><span data-stu-id="c6457-182">A notification sends an email to one or more addresses.</span></span>  <span data-ttu-id="c6457-183">Исправление позволяет запустить Runbook в службе автоматизации Azure, чтобы попытаться устранить обнаруженную проблему.</span><span class="sxs-lookup"><span data-stu-id="c6457-183">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span></span>

<span data-ttu-id="c6457-184">Структура действий оповещений приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="c6457-184">Alert actions have the following structure.</span></span>  <span data-ttu-id="c6457-185">Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров.</span><span class="sxs-lookup"><span data-stu-id="c6457-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 



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

<span data-ttu-id="c6457-186">В следующей таблице описаны свойства ресурсов действия оповещения.</span><span class="sxs-lookup"><span data-stu-id="c6457-186">The properties for Alert action resources are described in the following tables.</span></span>

| <span data-ttu-id="c6457-187">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c6457-187">Element name</span></span> | <span data-ttu-id="c6457-188">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c6457-188">Required</span></span> | <span data-ttu-id="c6457-189">Описание</span><span class="sxs-lookup"><span data-stu-id="c6457-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="c6457-190">Тип</span><span class="sxs-lookup"><span data-stu-id="c6457-190">Type</span></span> | <span data-ttu-id="c6457-191">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-191">Yes</span></span> | <span data-ttu-id="c6457-192">Тип действия.</span><span class="sxs-lookup"><span data-stu-id="c6457-192">Type of the action.</span></span>  <span data-ttu-id="c6457-193">Для действий оповещения это будет **Alert**.</span><span class="sxs-lookup"><span data-stu-id="c6457-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="c6457-194">Имя</span><span class="sxs-lookup"><span data-stu-id="c6457-194">Name</span></span> | <span data-ttu-id="c6457-195">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-195">Yes</span></span> | <span data-ttu-id="c6457-196">Отображаемое имя оповещения.</span><span class="sxs-lookup"><span data-stu-id="c6457-196">Display name for the alert.</span></span>  <span data-ttu-id="c6457-197">Это имя, которое отображается в консоли для правила генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="c6457-197">This is the name that's displayed in the console for the alert rule.</span></span> |
| <span data-ttu-id="c6457-198">Описание</span><span class="sxs-lookup"><span data-stu-id="c6457-198">Description</span></span> | <span data-ttu-id="c6457-199">Нет</span><span class="sxs-lookup"><span data-stu-id="c6457-199">No</span></span> | <span data-ttu-id="c6457-200">Необязательное описание оповещения.</span><span class="sxs-lookup"><span data-stu-id="c6457-200">Optional description of the alert.</span></span> |
| <span data-ttu-id="c6457-201">Severity</span><span class="sxs-lookup"><span data-stu-id="c6457-201">Severity</span></span> | <span data-ttu-id="c6457-202">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-202">Yes</span></span> | <span data-ttu-id="c6457-203">Серьезность записи оповещения состоит из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="c6457-203">Severity of the alert record from the following values:</span></span><br><br> <span data-ttu-id="c6457-204">**Critical**</span><span class="sxs-lookup"><span data-stu-id="c6457-204">**Critical**</span></span><br><span data-ttu-id="c6457-205">**Предупреждение;**</span><span class="sxs-lookup"><span data-stu-id="c6457-205">**Warning**</span></span><br><span data-ttu-id="c6457-206">**Informational**</span><span class="sxs-lookup"><span data-stu-id="c6457-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="c6457-207">Threshold (Пороговое значение)</span><span class="sxs-lookup"><span data-stu-id="c6457-207">Threshold</span></span>
<span data-ttu-id="c6457-208">Это обязательный раздел.</span><span class="sxs-lookup"><span data-stu-id="c6457-208">This section is required.</span></span>  <span data-ttu-id="c6457-209">Он определяет свойства порога оповещения.</span><span class="sxs-lookup"><span data-stu-id="c6457-209">It defines the properties for the alert threshold.</span></span>

| <span data-ttu-id="c6457-210">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c6457-210">Element name</span></span> | <span data-ttu-id="c6457-211">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c6457-211">Required</span></span> | <span data-ttu-id="c6457-212">Описание</span><span class="sxs-lookup"><span data-stu-id="c6457-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="c6457-213">Оператор</span><span class="sxs-lookup"><span data-stu-id="c6457-213">Operator</span></span> | <span data-ttu-id="c6457-214">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-214">Yes</span></span> | <span data-ttu-id="c6457-215">Оператор сравнения может содержать следующие значения:</span><span class="sxs-lookup"><span data-stu-id="c6457-215">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="c6457-216">**gt — больше;<br>lt — меньше.**</span><span class="sxs-lookup"><span data-stu-id="c6457-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="c6457-217">Значение</span><span class="sxs-lookup"><span data-stu-id="c6457-217">Value</span></span> | <span data-ttu-id="c6457-218">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-218">Yes</span></span> | <span data-ttu-id="c6457-219">Значение для сравнения с результатами.</span><span class="sxs-lookup"><span data-stu-id="c6457-219">The value to compare the results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="c6457-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="c6457-220">MetricsTrigger</span></span>
<span data-ttu-id="c6457-221">Это необязательный раздел.</span><span class="sxs-lookup"><span data-stu-id="c6457-221">This section is optional.</span></span>  <span data-ttu-id="c6457-222">Он добавляется для оповещения об измерении метрики.</span><span class="sxs-lookup"><span data-stu-id="c6457-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="c6457-223">Оповещения об измерении метрики в настоящее время находятся на этапе общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="c6457-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="c6457-224">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c6457-224">Element name</span></span> | <span data-ttu-id="c6457-225">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c6457-225">Required</span></span> | <span data-ttu-id="c6457-226">Описание</span><span class="sxs-lookup"><span data-stu-id="c6457-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="c6457-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="c6457-227">TriggerCondition</span></span> | <span data-ttu-id="c6457-228">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-228">Yes</span></span> | <span data-ttu-id="c6457-229">Указывает, задает ли порог общее число нарушений или число последовательных нарушений посредством следующих значений:</span><span class="sxs-lookup"><span data-stu-id="c6457-229">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span></span><br><br><span data-ttu-id="c6457-230">**Total;<br>Consecutive.**</span><span class="sxs-lookup"><span data-stu-id="c6457-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="c6457-231">Оператор</span><span class="sxs-lookup"><span data-stu-id="c6457-231">Operator</span></span> | <span data-ttu-id="c6457-232">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-232">Yes</span></span> | <span data-ttu-id="c6457-233">Оператор сравнения может содержать следующие значения:</span><span class="sxs-lookup"><span data-stu-id="c6457-233">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="c6457-234">**gt — больше;<br>lt — меньше.**</span><span class="sxs-lookup"><span data-stu-id="c6457-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="c6457-235">Значение</span><span class="sxs-lookup"><span data-stu-id="c6457-235">Value</span></span> | <span data-ttu-id="c6457-236">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-236">Yes</span></span> | <span data-ttu-id="c6457-237">Определяет, сколько раз должны быть соблюдены условия для активации оповещения.</span><span class="sxs-lookup"><span data-stu-id="c6457-237">Number of the times the criteria must be met to trigger the alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="c6457-238">Регулирование</span><span class="sxs-lookup"><span data-stu-id="c6457-238">Throttling</span></span>
<span data-ttu-id="c6457-239">Это необязательный раздел.</span><span class="sxs-lookup"><span data-stu-id="c6457-239">This section is optional.</span></span>  <span data-ttu-id="c6457-240">Добавьте этот раздел, если некоторое время после создания оповещения тем же правилом его не нужно отображать.</span><span class="sxs-lookup"><span data-stu-id="c6457-240">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="c6457-241">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c6457-241">Element name</span></span> | <span data-ttu-id="c6457-242">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c6457-242">Required</span></span> | <span data-ttu-id="c6457-243">Описание</span><span class="sxs-lookup"><span data-stu-id="c6457-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="c6457-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="c6457-244">DurationInMinutes</span></span> | <span data-ttu-id="c6457-245">Значение Yes, если добавлен элемент Throttling.</span><span class="sxs-lookup"><span data-stu-id="c6457-245">Yes if Throttling element included</span></span> | <span data-ttu-id="c6457-246">Количество минут, в течение которых оповещение не отображается после его создания тем же правилом генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="c6457-246">Number of minutes to suppress alerts after one from the same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="c6457-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="c6457-247">EmailNotification</span></span>
 <span data-ttu-id="c6457-248">Этот раздел является необязательным. Добавьте его, если требуется, чтобы оповещение отправляло электронное сообщение одному или нескольким получателям.</span><span class="sxs-lookup"><span data-stu-id="c6457-248">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span></span>

| <span data-ttu-id="c6457-249">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c6457-249">Element name</span></span> | <span data-ttu-id="c6457-250">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c6457-250">Required</span></span> | <span data-ttu-id="c6457-251">Описание</span><span class="sxs-lookup"><span data-stu-id="c6457-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="c6457-252">Recipients</span><span class="sxs-lookup"><span data-stu-id="c6457-252">Recipients</span></span> | <span data-ttu-id="c6457-253">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-253">Yes</span></span> | <span data-ttu-id="c6457-254">Разделенный запятыми список электронных адресов для отправки уведомления при создании оповещения, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="c6457-254">Comma delimited list of email addresses to send notification when an alert is created such as in the following example.</span></span><br><br><span data-ttu-id="c6457-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="c6457-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="c6457-256">Субъект</span><span class="sxs-lookup"><span data-stu-id="c6457-256">Subject</span></span> | <span data-ttu-id="c6457-257">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-257">Yes</span></span> | <span data-ttu-id="c6457-258">Строка темы электронного сообщения.</span><span class="sxs-lookup"><span data-stu-id="c6457-258">Subject line of the mail.</span></span> |
| <span data-ttu-id="c6457-259">Вложение</span><span class="sxs-lookup"><span data-stu-id="c6457-259">Attachment</span></span> | <span data-ttu-id="c6457-260">Нет</span><span class="sxs-lookup"><span data-stu-id="c6457-260">No</span></span> | <span data-ttu-id="c6457-261">Вложения в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="c6457-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="c6457-262">Если этот элемент добавлен, он должен иметь значение **None**.</span><span class="sxs-lookup"><span data-stu-id="c6457-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="c6457-263">Исправление</span><span class="sxs-lookup"><span data-stu-id="c6457-263">Remediation</span></span>
<span data-ttu-id="c6457-264">Этот раздел является необязательным. Добавьте его, если требуется, чтобы в ответ на оповещение запускался Runbook.</span><span class="sxs-lookup"><span data-stu-id="c6457-264">This section is optional  Include it if you want a runbook to start in response to the alert.</span></span> |

| <span data-ttu-id="c6457-265">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c6457-265">Element name</span></span> | <span data-ttu-id="c6457-266">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c6457-266">Required</span></span> | <span data-ttu-id="c6457-267">Описание</span><span class="sxs-lookup"><span data-stu-id="c6457-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="c6457-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="c6457-268">RunbookName</span></span> | <span data-ttu-id="c6457-269">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-269">Yes</span></span> | <span data-ttu-id="c6457-270">Имя запускаемого модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="c6457-270">Name of the runbook to start.</span></span> |
| <span data-ttu-id="c6457-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="c6457-271">WebhookUri</span></span> | <span data-ttu-id="c6457-272">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-272">Yes</span></span> | <span data-ttu-id="c6457-273">Универсальный код ресурса (URI) webhook для Runbook.</span><span class="sxs-lookup"><span data-stu-id="c6457-273">Uri of the webhook for the runbook.</span></span> |
| <span data-ttu-id="c6457-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="c6457-274">Expiry</span></span> | <span data-ttu-id="c6457-275">Нет</span><span class="sxs-lookup"><span data-stu-id="c6457-275">No</span></span> | <span data-ttu-id="c6457-276">Дата и время истечения срока действия исправления.</span><span class="sxs-lookup"><span data-stu-id="c6457-276">Date and time that the remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="c6457-277">Действия webhook</span><span class="sxs-lookup"><span data-stu-id="c6457-277">Webhook actions</span></span>

<span data-ttu-id="c6457-278">Действия webhook запускают процесс путем вызова URL-адреса и, при необходимости, предоставления полезных данных для отправки.</span><span class="sxs-lookup"><span data-stu-id="c6457-278">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span> <span data-ttu-id="c6457-279">Они похожи на действия исправления, но предназначены для объектов webhook, которые могут вызывать процессы, отличные от модулей Runbook службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="c6457-279">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="c6457-280">Они также включают дополнительную возможность предоставления полезных данных, доставляемых в удаленный процесс.</span><span class="sxs-lookup"><span data-stu-id="c6457-280">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="c6457-281">Если оповещение будет вызывать webhook, то помимо ресурса действия **Alert** ему требуется ресурс действия типа **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="c6457-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span></span>  

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

<span data-ttu-id="c6457-282">В следующей таблице описаны свойства ресурсов действия webhook.</span><span class="sxs-lookup"><span data-stu-id="c6457-282">The properties for Webhook action resources are described in the following tables.</span></span>

| <span data-ttu-id="c6457-283">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c6457-283">Element name</span></span> | <span data-ttu-id="c6457-284">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c6457-284">Required</span></span> | <span data-ttu-id="c6457-285">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="c6457-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="c6457-286">type</span><span class="sxs-lookup"><span data-stu-id="c6457-286">type</span></span> | <span data-ttu-id="c6457-287">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-287">Yes</span></span> | <span data-ttu-id="c6457-288">Тип действия.</span><span class="sxs-lookup"><span data-stu-id="c6457-288">Type of the action.</span></span>  <span data-ttu-id="c6457-289">Для действий webhook это будет **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="c6457-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="c6457-290">name</span><span class="sxs-lookup"><span data-stu-id="c6457-290">name</span></span> | <span data-ttu-id="c6457-291">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-291">Yes</span></span> | <span data-ttu-id="c6457-292">Отображаемое имя действия.</span><span class="sxs-lookup"><span data-stu-id="c6457-292">Display name for the action.</span></span>  <span data-ttu-id="c6457-293">Оно не отображается в консоли.</span><span class="sxs-lookup"><span data-stu-id="c6457-293">This is not displayed in the console.</span></span> |
| <span data-ttu-id="c6457-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="c6457-294">wehookUri</span></span> | <span data-ttu-id="c6457-295">Да</span><span class="sxs-lookup"><span data-stu-id="c6457-295">Yes</span></span> | <span data-ttu-id="c6457-296">Универсальный код ресурса (URI) webhook.</span><span class="sxs-lookup"><span data-stu-id="c6457-296">Uri for the webhook.</span></span> |
| <span data-ttu-id="c6457-297">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="c6457-297">customPayload</span></span> | <span data-ttu-id="c6457-298">Нет</span><span class="sxs-lookup"><span data-stu-id="c6457-298">No</span></span> | <span data-ttu-id="c6457-299">Пользовательские полезные данные, отправляемые в объект webhook.</span><span class="sxs-lookup"><span data-stu-id="c6457-299">Custom payload to be sent to the webhook.</span></span> <span data-ttu-id="c6457-300">Формат зависит от данных, ожидаемых объектом webhook.</span><span class="sxs-lookup"><span data-stu-id="c6457-300">The format will depend on what the webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="c6457-301">Образец</span><span class="sxs-lookup"><span data-stu-id="c6457-301">Sample</span></span>

<span data-ttu-id="c6457-302">Ниже приведен пример решения со приведенными ниже ресурсами.</span><span class="sxs-lookup"><span data-stu-id="c6457-302">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="c6457-303">Сохраненный поиск</span><span class="sxs-lookup"><span data-stu-id="c6457-303">Saved search</span></span>
- <span data-ttu-id="c6457-304">Расписание</span><span class="sxs-lookup"><span data-stu-id="c6457-304">Schedule</span></span>
- <span data-ttu-id="c6457-305">Действие оповещения</span><span class="sxs-lookup"><span data-stu-id="c6457-305">Alert action</span></span>
- <span data-ttu-id="c6457-306">Действия webhook</span><span class="sxs-lookup"><span data-stu-id="c6457-306">Webhook action</span></span>

<span data-ttu-id="c6457-307">В примере используются переменные [стандартных параметров решения](operations-management-suite-solutions-solution-file.md#parameters), что является общепринятой практикой для решений, в отличие от жестко программируемых значений в определениях ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c6457-307">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>

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
              "Description": "List of recipients for the email alert separated by semicolon"
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


<span data-ttu-id="c6457-308">Следующий файл параметров содержит примеры значений для такого решения.</span><span class="sxs-lookup"><span data-stu-id="c6457-308">The following parameter file provides samples values for this solution.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="c6457-309">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6457-309">Next steps</span></span>
* <span data-ttu-id="c6457-310">[Добавьте представления](operations-management-suite-solutions-resources-views.md) в решение для управления.</span><span class="sxs-lookup"><span data-stu-id="c6457-310">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="c6457-311">[Добавьте модули Runbook и другие ресурсы службы автоматизации](operations-management-suite-solutions-resources-automation.md) в решение для управления.</span><span class="sxs-lookup"><span data-stu-id="c6457-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>

