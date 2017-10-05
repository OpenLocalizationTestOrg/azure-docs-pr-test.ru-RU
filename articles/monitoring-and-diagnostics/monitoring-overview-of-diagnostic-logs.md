---
title: "Обзор журналов диагностики Azure | Документация Майкрософт"
description: "Узнайте, что такое журналы диагностики Azure и как их использовать для просмотра событий, происходящих в ресурсе Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: d59abde29fc7b73a799e5bf3659b02f824b693de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="e7efe-103">Сбор и использование данных журнала из ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="e7efe-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="e7efe-104">Что такое журналы диагностики ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="e7efe-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="e7efe-105">**Журналы диагностики уровня ресурсов Azure** генерируются ресурсом. Они содержат подробные и своевременные данные об операциях этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="e7efe-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span></span> <span data-ttu-id="e7efe-106">Содержимое этих журналов зависит от типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="e7efe-106">The content of these logs varies by resource type.</span></span> <span data-ttu-id="e7efe-107">Например, счетчики правила группы безопасности сети и аудит Key Vault представляют две категории журналов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e7efe-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="e7efe-108">Журналы диагностики уровня ресурса отличаются от [журнала действий](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e7efe-108">Resource-level diagnostic logs differ from the [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="e7efe-109">Журнал действий содержит информацию об операциях, которые были выполнены с ресурсами в вашей подписке с помощью Resource Manager, например о создании виртуальной машины или удалении приложения логики.</span><span class="sxs-lookup"><span data-stu-id="e7efe-109">The Activity Log provides insight into the operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="e7efe-110">Журнал действий — это журнал уровня подписки.</span><span class="sxs-lookup"><span data-stu-id="e7efe-110">The Activity Log is a subscription-level log.</span></span> <span data-ttu-id="e7efe-111">Журналы диагностики уровня ресурса дают представление об операциях, которые были выполнены в рамках этого ресурса, например о получении секрета из Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e7efe-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="e7efe-112">Журналы диагностики уровня ресурса также отличаются от журналов диагностики уровня гостевой ОС.</span><span class="sxs-lookup"><span data-stu-id="e7efe-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="e7efe-113">Журналы диагностики гостевой ОС собирает агент, работающий на виртуальной машине или поддерживаемом ресурсе другого типа.</span><span class="sxs-lookup"><span data-stu-id="e7efe-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="e7efe-114">Для сбора журналов диагностики уровня ресурса не требуется агент. В них записываются данные ресурсов из платформы Azure, тогда как в журналы диагностики уровня гостевой ОС записываются данные из операционной системы и приложений, выполняющихся на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e7efe-114">Resource-level diagnostic logs require no agent and capture resource-specific data from the Azure platform itself, while guest OS-level diagnostic logs capture data from the operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="e7efe-115">Не все ресурсы поддерживают описанный здесь новый тип журналов диагностики ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e7efe-115">Not all resources support the new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="e7efe-116">Эта статья содержит раздел со списком типов ресурсов, поддерживающих новые журналы диагностики уровня ресурса.</span><span class="sxs-lookup"><span data-stu-id="e7efe-116">This article contains a section listing which resource types support the new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="e7efe-117">Журналы диагностики ресурсов и другие типы журналов</span><span class="sxs-lookup"><span data-stu-id="e7efe-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="e7efe-118">Что можно делать с журналами диагностики уровня ресурса</span><span class="sxs-lookup"><span data-stu-id="e7efe-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="e7efe-119">Ниже описано несколько доступных операций с журналами диагностики ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e7efe-119">Here are some of the things you can do with resource diagnostic logs:</span></span>

![Логическое размещение журналов диагностики ресурсов](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="e7efe-121">Сохранение журналов в [**учетную запись хранения**](monitoring-archive-diagnostic-logs.md) для аудита или проверки вручную.</span><span class="sxs-lookup"><span data-stu-id="e7efe-121">Save them to a [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="e7efe-122">В **параметрах диагностики ресурсов** можно задать время хранения (в днях).</span><span class="sxs-lookup"><span data-stu-id="e7efe-122">You can specify the retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="e7efe-123">[Потоковая передача журналов в **концентраторы событий**](monitoring-stream-diagnostic-logs-to-event-hubs.md) для обработки в сторонней службе или пользовательском аналитическом решении, например в PowerBI.</span><span class="sxs-lookup"><span data-stu-id="e7efe-123">[Stream them to **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="e7efe-124">Анализ журналов с помощью [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="e7efe-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="e7efe-125">Вы можете использовать учетную запись хранения или пространство имен концентраторов событий, не входящее в подписку, в которой создаются журналы.</span><span class="sxs-lookup"><span data-stu-id="e7efe-125">You can use a storage account or Event Hubs namespace that is not in the same subscription as the one emitting logs.</span></span> <span data-ttu-id="e7efe-126">Пользователю, который настраивает этот параметр, должен быть предоставлен соответствующий уровень доступа RBAC к обеим подпискам.</span><span class="sxs-lookup"><span data-stu-id="e7efe-126">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="e7efe-127">Параметры диагностики ресурсов</span><span class="sxs-lookup"><span data-stu-id="e7efe-127">Resource diagnostic settings</span></span>
<span data-ttu-id="e7efe-128">Журналы диагностики для всех ресурсов, кроме вычислительных, настраиваются с помощью параметров диагностики ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e7efe-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="e7efe-129">**Параметры диагностики ресурсов** для управления ресурсами:</span><span class="sxs-lookup"><span data-stu-id="e7efe-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="e7efe-130">Куда отправляются журналы диагностики ресурсов и метрики (учетная запись хранения, концентраторы событий и/или OMS Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="e7efe-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="e7efe-131">Какие категории журнала отправляются и следует ли отправлять данные метрики.</span><span class="sxs-lookup"><span data-stu-id="e7efe-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="e7efe-132">Как долго должны храниться журналы каждой категории в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e7efe-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="e7efe-133">Срок хранения 0 дней означает, что журналы хранятся неограниченно долго.</span><span class="sxs-lookup"><span data-stu-id="e7efe-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="e7efe-134">В противном случае укажите количество дней в диапазоне от 1 до 2 147 483 647.</span><span class="sxs-lookup"><span data-stu-id="e7efe-134">Otherwise, the value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="e7efe-135">Если политики хранения заданы, но хранение журналов в учетной записи хранения отключено (например, выбраны только варианты концентраторов событий или OMS), политики хранения не будут применены.</span><span class="sxs-lookup"><span data-stu-id="e7efe-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span></span>
    - <span data-ttu-id="e7efe-136">Политики хранения применяются по дням, поэтому в конце дня (по времени в формате UTC) журналы, срок которых теперь превышает период хранения, будут удалены.</span><span class="sxs-lookup"><span data-stu-id="e7efe-136">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span></span> <span data-ttu-id="e7efe-137">Например, если настроена политика хранения в течение одного дня, то в начале текущего дня журналы за вчерашний день будет удалены.</span><span class="sxs-lookup"><span data-stu-id="e7efe-137">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span>

<span data-ttu-id="e7efe-138">Эти параметры легко настраиваются в параметрах диагностики для ресурса на портале Azure, а также с помощью Azure PowerShell, команд интерфейса командной строки или с помощью статьи [REST API Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7efe-138">These settings are easily configured via the diagnostic settings for a resource in the Azure portal, via Azure PowerShell and CLI commands, or via the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="e7efe-139">В журналах диагностики и метрик с уровня гостевой ОС для вычислительных ресурсов (например, виртуальных машин или Service Fabric) доступен [отдельный механизм настройки и выбора выходных данных](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="e7efe-139">Diagnostic logs and metrics for from the guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-to-enable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="e7efe-140">Как включить сбор журналов диагностики ресурсов</span><span class="sxs-lookup"><span data-stu-id="e7efe-140">How to enable collection of resource diagnostic logs</span></span>
<span data-ttu-id="e7efe-141">Сбор журналов диагностики ресурсов можно включить [во время создания ресурса с помощью шаблона Resource Manager](./monitoring-enable-diagnostic-logs-using-template.md) или после его создания на странице ресурса на портале.</span><span class="sxs-lookup"><span data-stu-id="e7efe-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in the portal.</span></span> <span data-ttu-id="e7efe-142">Сбор этих журналов можно также включить в любой момент с помощью Azure PowerShell, команд интерфейса командной строки или REST API Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="e7efe-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using the Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="e7efe-143">При работе с некоторыми ресурсами эти инструкции могут требовать корректировки.</span><span class="sxs-lookup"><span data-stu-id="e7efe-143">These instructions may not apply directly to every resource.</span></span> <span data-ttu-id="e7efe-144">Изучите связи на схеме, представленной в конце этой страницы, чтобы разобраться в дополнительных действиях, которые могут потребоваться при использовании некоторых типов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e7efe-144">See the schema links at the bottom of this page to understand special steps that may apply to certain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-the-portal"></a><span data-ttu-id="e7efe-145">Включение сбора журналов диагностики ресурсов на портале</span><span class="sxs-lookup"><span data-stu-id="e7efe-145">Enable collection of resource diagnostic logs in the portal</span></span>
<span data-ttu-id="e7efe-146">Сбор журналов диагностики ресурсов на портале Azure после создания ресурса можно включить, перейдя к конкретному ресурсу или к Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="e7efe-146">You can enable collection of resource diagnostic logs in the Azure portal after a resource has been created either by going to a specific resource or by navigating to Azure Monitor.</span></span> <span data-ttu-id="e7efe-147">Чтобы выполнить это с помощью Azure Monitor, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e7efe-147">To enable this via Azure Monitor:</span></span>

1. <span data-ttu-id="e7efe-148">На [портале Azure](http://portal.azure.com) перейдите к Azure Monitor и щелкните **Параметры диагностики**</span><span class="sxs-lookup"><span data-stu-id="e7efe-148">In the [Azure portal](http://portal.azure.com), navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Раздел мониторинга Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="e7efe-150">При необходимости отфильтруйте список по группе или типу ресурса, а затем щелкните ресурс, для которого необходимо задать параметр диагностики.</span><span class="sxs-lookup"><span data-stu-id="e7efe-150">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="e7efe-151">Если параметров для выбранного ресурса не существует, вам будет предложено создать параметр.</span><span class="sxs-lookup"><span data-stu-id="e7efe-151">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="e7efe-152">Щелкните Turn on diagnostics (Включить диагностику).</span><span class="sxs-lookup"><span data-stu-id="e7efe-152">Click "Turn on diagnostics."</span></span>

   ![Добавление параметра диагностики — имеющиеся параметры отсутствуют](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="e7efe-154">Если в ресурсе имеются параметры, для него отобразится список настроенных параметров.</span><span class="sxs-lookup"><span data-stu-id="e7efe-154">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="e7efe-155">Нажмите Add diagnostic setting (Добавить параметр диагностики).</span><span class="sxs-lookup"><span data-stu-id="e7efe-155">Click "Add diagnostic setting."</span></span>

   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="e7efe-157">Задайте имя параметра, установите флажки для каждого целевого расположения, в которое необходимо отправить данные, и укажите ресурс, используемый для каждого назначения.</span><span class="sxs-lookup"><span data-stu-id="e7efe-157">Give your setting a name, check the boxes for each destination to which you would like to send data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="e7efe-158">При необходимости с помощью ползунков **Хранение (дни)** укажите продолжительность хранения этих журналов в днях (применимо только к целевому расположению учетной записи хранения).</span><span class="sxs-lookup"><span data-stu-id="e7efe-158">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders (only applicable to the storage account destination).</span></span> <span data-ttu-id="e7efe-159">Нулевое значение означает, что журналы будут храниться неограниченно долго.</span><span class="sxs-lookup"><span data-stu-id="e7efe-159">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="e7efe-161">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e7efe-161">Click **Save**.</span></span>

<span data-ttu-id="e7efe-162">Через несколько секунд появится новый параметр в списке параметров для данного ресурса, и сразу же после создания данных о событии журналы диагностики отправятся по указанным назначениям.</span><span class="sxs-lookup"><span data-stu-id="e7efe-162">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are sent to the specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="e7efe-163">Включение сбора журналов диагностики ресурсов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7efe-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="e7efe-164">Чтобы включить сбор журналов диагностики ресурсов с помощью Azure PowerShell, используйте следующие команды.</span><span class="sxs-lookup"><span data-stu-id="e7efe-164">To enable collection of resource diagnostic logs via Azure PowerShell, use the following commands:</span></span>

<span data-ttu-id="e7efe-165">Выполните приведенную ниже команду, чтобы включить отправку журналов диагностики в учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e7efe-165">To enable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="e7efe-166">StorageAccountId — это идентификатор ресурса учетной записи хранения, в которую будут отправляться журналы.</span><span class="sxs-lookup"><span data-stu-id="e7efe-166">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="e7efe-167">Чтобы включить потоковую передачу журналов диагностики в концентратор событий, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e7efe-167">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="e7efe-168">ServiceBusRuleID — это строка в формате `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="e7efe-168">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="e7efe-169">Чтобы включить отправку журналов диагностики в рабочую область Log Analytics, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e7efe-169">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
```

<span data-ttu-id="e7efe-170">Идентификатор ресурса рабочей области Log Analytics можно получить с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="e7efe-170">You can obtain the resource ID of your Log Analytics workspace using the following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="e7efe-171">Можно объединять эти параметры, чтобы получить несколько вариантов вывода.</span><span class="sxs-lookup"><span data-stu-id="e7efe-171">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="e7efe-172">Включение сбора журналов диагностики ресурсов с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="e7efe-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="e7efe-173">Чтобы включить сбор журналов диагностики ресурсов с помощью Azure CLI, используйте следующие команды.</span><span class="sxs-lookup"><span data-stu-id="e7efe-173">To enable collection of resource diagnostic logs via the Azure CLI, use the following commands:</span></span>

<span data-ttu-id="e7efe-174">Выполните приведенную ниже команду, чтобы включить отправку журналов диагностики в учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e7efe-174">To enable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="e7efe-175">StorageAccountId — это идентификатор ресурса учетной записи хранения, в которую будут отправляться журналы.</span><span class="sxs-lookup"><span data-stu-id="e7efe-175">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="e7efe-176">Чтобы включить потоковую передачу журналов диагностики в концентратор событий, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e7efe-176">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="e7efe-177">ServiceBusRuleID — это строка в формате `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="e7efe-177">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="e7efe-178">Чтобы включить отправку журналов диагностики в рабочую область Log Analytics, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e7efe-178">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
```

<span data-ttu-id="e7efe-179">Можно объединять эти параметры, чтобы получить несколько вариантов вывода.</span><span class="sxs-lookup"><span data-stu-id="e7efe-179">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="e7efe-180">Включение сбора журналов диагностики ресурсов с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="e7efe-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="e7efe-181">Изменение параметров диагностики с помощью REST API Azure Monitor описано в [этом документе](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7efe-181">To change diagnostic settings using the Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-the-portal"></a><span data-ttu-id="e7efe-182">Управление параметрами диагностики ресурсов на портале</span><span class="sxs-lookup"><span data-stu-id="e7efe-182">Manage resource diagnostic settings in the portal</span></span>
<span data-ttu-id="e7efe-183">Убедитесь, что все ресурсы настроены с помощью параметров диагностики.</span><span class="sxs-lookup"><span data-stu-id="e7efe-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="e7efe-184">Перейдите к разделу **Монитор** на портале и откройте **Параметры диагностики**.</span><span class="sxs-lookup"><span data-stu-id="e7efe-184">Navigate to **Monitor** in the portal and open **Diagnostic settings**.</span></span>

![Колонка "Журналы диагностики" на портале](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="e7efe-186">Чтобы найти раздел "Мониторинг", может понадобиться щелкнуть "Больше служб".</span><span class="sxs-lookup"><span data-stu-id="e7efe-186">You may have to click "More services" to find the Monitor section.</span></span>

<span data-ttu-id="e7efe-187">Здесь можно просматривать и фильтровать все ресурсы, поддерживающие журналы диагностики. Таким образом можно проверить, включена ли для них диагностика.</span><span class="sxs-lookup"><span data-stu-id="e7efe-187">Here you can view and filter all resources that support diagnostic settings to see if they have diagnostics enabled.</span></span> <span data-ttu-id="e7efe-188">Вы также можете детально просмотреть сведения, чтобы проверить, задано ли для ресурса несколько параметров, в какую учетную запись хранения, пространство имен концентраторов событий и/или рабочую область Log Analytics передаются данные.</span><span class="sxs-lookup"><span data-stu-id="e7efe-188">You can also drill down to see if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Журналы диагностики на портале](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="e7efe-190">При добавлении параметра диагностики открывается колонка "Параметры диагностики", в которой можно включить, отключить или изменить параметры диагностики для выбранного ресурса.</span><span class="sxs-lookup"><span data-stu-id="e7efe-190">Adding a diagnostic setting brings up the Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for the selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="e7efe-191">Поддерживаемые службы, категории и схемы для журналов диагностики ресурсов</span><span class="sxs-lookup"><span data-stu-id="e7efe-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="e7efe-192">С полным списком поддерживаемых служб, категорий и схем журнала, используемых этими службами, ознакомьтесь в [этой статье](monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e7efe-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and the log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7efe-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e7efe-193">Next steps</span></span>

* [<span data-ttu-id="e7efe-194">Потоковая передача журналов диагностики Azure в **концентраторы событий**</span><span class="sxs-lookup"><span data-stu-id="e7efe-194">Stream resource diagnostic logs to **Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="e7efe-195">Создание или обновление диагностического параметра</span><span class="sxs-lookup"><span data-stu-id="e7efe-195">Change resource diagnostic settings using the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="e7efe-196">Сбор журналов и метрик для служб Azure для использования в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e7efe-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
