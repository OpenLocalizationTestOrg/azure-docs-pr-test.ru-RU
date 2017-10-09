---
title: "aaaArchive журналы диагностики Azure | Документы Microsoft"
description: "Узнайте, как tooarchive вашей Azure журналы диагностики для долгосрочного хранения в учетную запись хранилища."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a><span data-ttu-id="33956-103">Архивация журналов диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="33956-103">Archive Azure Diagnostic Logs</span></span>
<span data-ttu-id="33956-104">В этой статье показано, как использовать hello портал Azure, командлеты PowerShell, CLI, или REST API tooarchive вашей [Azure журналам диагностики](monitoring-overview-of-diagnostic-logs.md) в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="33956-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, CLI, or REST API tooarchive your [Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md) in a storage account.</span></span> <span data-ttu-id="33956-105">Этот параметр полезен, если вы хотите tooretain журналы вашей диагностики с политикой хранения необязательно для аудита, статического анализа или резервной копии.</span><span class="sxs-lookup"><span data-stu-id="33956-105">This option is useful if you would like tooretain your diagnostic logs with an optional retention policy for audit, static analysis, or backup.</span></span> <span data-ttu-id="33956-106">Учетная запись хранения Hello не имеет toobe в hello той же подписке, hello ресурсов выпуска журналы при условии, что hello пользователь, настраивающий приветствия имеет соответствующий RBAC доступа tooboth подписок.</span><span class="sxs-lookup"><span data-stu-id="33956-106">hello storage account does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33956-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="33956-107">Prerequisites</span></span>
<span data-ttu-id="33956-108">Прежде чем начать, вам потребуется слишком[создать учетную запись хранилища](../storage/storage-create-storage-account.md) toowhich, вы можете архивировать вашим журналам диагностики.</span><span class="sxs-lookup"><span data-stu-id="33956-108">Before you begin, you need too[create a storage account](../storage/storage-create-storage-account.md) toowhich you can archive your diagnostic logs.</span></span> <span data-ttu-id="33956-109">Настоятельно рекомендуется не использовать существующую учетную запись хранения с других, отличных от наблюдения за данными, хранимыми в нем, чтобы лучше управлять toomonitoring доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="33956-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="33956-110">Тем не менее если ваш журнал действий и учетной записи хранения метрики диагностики tooa архивация также выполняется, может быть toouse смысле этой учетной записи хранения для вашей журналы диагностики также tookeep все данные наблюдения в центральном расположении.</span><span class="sxs-lookup"><span data-stu-id="33956-110">However, if you are also archiving your Activity Log and diagnostic metrics tooa storage account, it may make sense toouse that storage account for your diagnostic logs as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="33956-111">Hello учетной записи хранилища, используемого должна быть учетной записью хранения общего назначения, не учетную запись хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="33956-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span>

## <a name="diagnostic-settings"></a><span data-ttu-id="33956-112">Параметры диагностики</span><span class="sxs-lookup"><span data-stu-id="33956-112">Diagnostic settings</span></span>
<span data-ttu-id="33956-113">задать tooarchive журналы вашей диагностики с помощью приведенных ниже способов hello, **параметра диагностики** к определенному ресурсу.</span><span class="sxs-lookup"><span data-stu-id="33956-113">tooarchive your diagnostic logs using any of hello methods below, you set a **diagnostic setting** for a particular resource.</span></span> <span data-ttu-id="33956-114">Параметра диагностики для ресурса определяет категории hello журналов и данных метрики отправляются tooa назначения (учетной записи хранилища, пространство имен концентраторов событий или служба аналитики журналов).</span><span class="sxs-lookup"><span data-stu-id="33956-114">A diagnostic setting for a resource defines hello categories of logs and metric data sent tooa destination (storage account, Event Hubs namespace, or Log Analytics).</span></span> <span data-ttu-id="33956-115">Он также определяет политику хранения hello (количество дней tooretain) для событий по каждой категории журнала и метрик данные, хранящиеся в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="33956-115">It also defines hello retention policy (number of days tooretain) for events of each log category and metric data stored in a storage account.</span></span> <span data-ttu-id="33956-116">Если политика хранения toozero, события для этой категории журнала хранятся бесконечно (то есть, toosay, бесконечно).</span><span class="sxs-lookup"><span data-stu-id="33956-116">If a retention policy is set toozero, events for that log category are stored indefinitely (that is toosay, forever).</span></span> <span data-ttu-id="33956-117">Для политики хранения можно задать любое значение от 1 до 2 147 483 647.</span><span class="sxs-lookup"><span data-stu-id="33956-117">A retention policy can otherwise be any number of days between 1 and 2147483647.</span></span> <span data-ttu-id="33956-118">[Подробные сведения о параметрах диагностики см. здесь](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="33956-118">[You can read more about diagnostic settings here](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span> <span data-ttu-id="33956-119">Политики хранения, примененных в день, поэтому hello регистрирует конец дня (UTC), с датой hello, что теперь находится за пределами hello политики хранения будут удалены.</span><span class="sxs-lookup"><span data-stu-id="33956-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="33956-120">Например если политика хранения продолжительностью в один день, в начале hello сегодня день hello hello журналы из позавчерашнего дня hello, будет удален</span><span class="sxs-lookup"><span data-stu-id="33956-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted</span></span>

## <a name="archive-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="33956-121">Журналы диагностики архив с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="33956-121">Archive diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="33956-122">На портале hello перейдите tooAzure монитор и нажмите на **параметров диагностики**</span><span class="sxs-lookup"><span data-stu-id="33956-122">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Раздел мониторинга Azure Monitor](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="33956-124">При необходимости фильтровать список hello по группе ресурсов или тип ресурса, а затем щелкните hello ресурсов, для которого вы хотите tooset параметра диагностики.</span><span class="sxs-lookup"><span data-stu-id="33956-124">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="33956-125">Если параметры не существует в hello ресурс, который вы выбрали, не запрошенные toocreate параметр.</span><span class="sxs-lookup"><span data-stu-id="33956-125">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="33956-126">Щелкните Turn on diagnostics (Включить диагностику).</span><span class="sxs-lookup"><span data-stu-id="33956-126">Click "Turn on diagnostics."</span></span>

   ![Добавление параметра диагностики — имеющиеся параметры отсутствуют](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="33956-128">Если имеются существующие параметры ресурсов hello, вы увидите список параметров, уже настроен на этом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="33956-128">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="33956-129">Нажмите Add diagnostic setting (Добавить параметр диагностики).</span><span class="sxs-lookup"><span data-stu-id="33956-129">Click "Add diagnostic setting."</span></span>

   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="33956-131">Введите имя параметра и установите флажок "hello" для **Экспорт tooStorage учетной записи**, затем выберите учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="33956-131">Give your setting a name and check hello box for **Export tooStorage Account**, then select a storage account.</span></span> <span data-ttu-id="33956-132">При необходимости задайте количество дней tooretain эти журналы с помощью hello **хранения (в днях)** ползунки.</span><span class="sxs-lookup"><span data-stu-id="33956-132">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders.</span></span> <span data-ttu-id="33956-133">Хранение 0 дней хранит журналы hello бесконечно.</span><span class="sxs-lookup"><span data-stu-id="33956-133">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="33956-135">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="33956-135">Click **Save**.</span></span>

<span data-ttu-id="33956-136">Через несколько секунд появится новый параметр hello в списке параметров для данного ресурса и журналы диагностики, хранения архивных toothat учетной записи, как только создается новый данные события.</span><span class="sxs-lookup"><span data-stu-id="33956-136">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are archived toothat storage account as soon as new event data is generated.</span></span>

## <a name="archive-diagnostic-logs-via-azure-powershell"></a><span data-ttu-id="33956-137">Архивация журналов диагностики с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="33956-137">Archive diagnostic logs via Azure PowerShell</span></span>
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| <span data-ttu-id="33956-138">Свойство</span><span class="sxs-lookup"><span data-stu-id="33956-138">Property</span></span> | <span data-ttu-id="33956-139">Обязательно</span><span class="sxs-lookup"><span data-stu-id="33956-139">Required</span></span> | <span data-ttu-id="33956-140">Описание</span><span class="sxs-lookup"><span data-stu-id="33956-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33956-141">ResourceId</span><span class="sxs-lookup"><span data-stu-id="33956-141">ResourceId</span></span> |<span data-ttu-id="33956-142">Да</span><span class="sxs-lookup"><span data-stu-id="33956-142">Yes</span></span> |<span data-ttu-id="33956-143">Идентификатор ресурса hello ресурса, на котором будет tooset параметра диагностики.</span><span class="sxs-lookup"><span data-stu-id="33956-143">Resource ID of hello resource on which you want tooset a diagnostic setting.</span></span> |
| <span data-ttu-id="33956-144">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="33956-144">StorageAccountId</span></span> |<span data-ttu-id="33956-145">Нет</span><span class="sxs-lookup"><span data-stu-id="33956-145">No</span></span> |<span data-ttu-id="33956-146">Идентификатор ресурса toowhich hello учетной записи хранения журналов диагностики должен быть сохранен.</span><span class="sxs-lookup"><span data-stu-id="33956-146">Resource ID of hello Storage Account toowhich Diagnostic Logs should be saved.</span></span> |
| <span data-ttu-id="33956-147">Категории</span><span class="sxs-lookup"><span data-stu-id="33956-147">Categories</span></span> |<span data-ttu-id="33956-148">Нет</span><span class="sxs-lookup"><span data-stu-id="33956-148">No</span></span> |<span data-ttu-id="33956-149">Список разделенных запятыми tooenable категории журнала.</span><span class="sxs-lookup"><span data-stu-id="33956-149">Comma-separated list of log categories tooenable.</span></span> |
| <span data-ttu-id="33956-150">Включено</span><span class="sxs-lookup"><span data-stu-id="33956-150">Enabled</span></span> |<span data-ttu-id="33956-151">Да</span><span class="sxs-lookup"><span data-stu-id="33956-151">Yes</span></span> |<span data-ttu-id="33956-152">Логическое значение, определяющее включение и отключение диагностики на этом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="33956-152">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |
| <span data-ttu-id="33956-153">RetentionEnabled</span><span class="sxs-lookup"><span data-stu-id="33956-153">RetentionEnabled</span></span> |<span data-ttu-id="33956-154">Нет</span><span class="sxs-lookup"><span data-stu-id="33956-154">No</span></span> |<span data-ttu-id="33956-155">Логическое значение, определяющее включение политики хранения на этом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="33956-155">Boolean indicating if a retention policy are enabled on this resource.</span></span> |
| <span data-ttu-id="33956-156">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="33956-156">RetentionInDays</span></span> |<span data-ttu-id="33956-157">Нет</span><span class="sxs-lookup"><span data-stu-id="33956-157">No</span></span> |<span data-ttu-id="33956-158">Количество дней, в течение которых будут храниться события: от 1 до 2 147 483 647.</span><span class="sxs-lookup"><span data-stu-id="33956-158">Number of days for which events should be retained between 1 and 2147483647.</span></span> <span data-ttu-id="33956-159">Нулевое значение хранятся журналы hello бесконечно.</span><span class="sxs-lookup"><span data-stu-id="33956-159">A value of zero stores hello logs indefinitely.</span></span> |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a><span data-ttu-id="33956-160">Журналы диагностики архив через hello кросс-платформенных CLI</span><span class="sxs-lookup"><span data-stu-id="33956-160">Archive diagnostic logs via hello Cross-Platform CLI</span></span>
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| <span data-ttu-id="33956-161">Свойство</span><span class="sxs-lookup"><span data-stu-id="33956-161">Property</span></span> | <span data-ttu-id="33956-162">Обязательно</span><span class="sxs-lookup"><span data-stu-id="33956-162">Required</span></span> | <span data-ttu-id="33956-163">Описание</span><span class="sxs-lookup"><span data-stu-id="33956-163">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33956-164">ResourceId</span><span class="sxs-lookup"><span data-stu-id="33956-164">resourceId</span></span> |<span data-ttu-id="33956-165">Да</span><span class="sxs-lookup"><span data-stu-id="33956-165">Yes</span></span> |<span data-ttu-id="33956-166">Идентификатор ресурса hello ресурса, на котором будет tooset параметра диагностики.</span><span class="sxs-lookup"><span data-stu-id="33956-166">Resource ID of hello resource on which you want tooset a diagnostic setting.</span></span> |
| <span data-ttu-id="33956-167">storageId</span><span class="sxs-lookup"><span data-stu-id="33956-167">storageId</span></span> |<span data-ttu-id="33956-168">Нет</span><span class="sxs-lookup"><span data-stu-id="33956-168">No</span></span> |<span data-ttu-id="33956-169">Журналы диагностики toowhich учетной записи хранилища hello идентификатор ресурса должен быть сохранен.</span><span class="sxs-lookup"><span data-stu-id="33956-169">Resource ID of hello Storage Account toowhich diagnostic logs should be saved.</span></span> |
| <span data-ttu-id="33956-170">Категории</span><span class="sxs-lookup"><span data-stu-id="33956-170">categories</span></span> |<span data-ttu-id="33956-171">Нет</span><span class="sxs-lookup"><span data-stu-id="33956-171">No</span></span> |<span data-ttu-id="33956-172">Список разделенных запятыми tooenable категории журнала.</span><span class="sxs-lookup"><span data-stu-id="33956-172">Comma-separated list of log categories tooenable.</span></span> |
| <span data-ttu-id="33956-173">Включено</span><span class="sxs-lookup"><span data-stu-id="33956-173">enabled</span></span> |<span data-ttu-id="33956-174">Да</span><span class="sxs-lookup"><span data-stu-id="33956-174">Yes</span></span> |<span data-ttu-id="33956-175">Логическое значение, определяющее включение и отключение диагностики на этом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="33956-175">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a><span data-ttu-id="33956-176">Журналы диагностики архив через API-Интерфейс REST hello</span><span class="sxs-lookup"><span data-stu-id="33956-176">Archive diagnostic logs via hello REST API</span></span>
<span data-ttu-id="33956-177">[См. в этом документе](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) сведения на как можно настроить параметра диагностики, с помощью API REST Azure монитор hello.</span><span class="sxs-lookup"><span data-stu-id="33956-177">[See this document](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) for information on how you can set up a diagnostic setting using hello Azure Monitor REST API.</span></span>

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a><span data-ttu-id="33956-178">Схема в журналах диагностики в учетной записи хранилища hello</span><span class="sxs-lookup"><span data-stu-id="33956-178">Schema of diagnostic logs in hello storage account</span></span>
<span data-ttu-id="33956-179">После настройки архивации, как только событие происходит в одну из категорий hello журнала, которые вы выбрали контейнер хранилища создается в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="33956-179">Once you have set up archival, a storage container is created in hello storage account as soon as an event occurs in one of hello log categories you have enabled.</span></span> <span data-ttu-id="33956-180">Hello большие двоичные объекты в контейнере hello следуйте hello в том же формате, в журналы диагностики и hello журнал действий.</span><span class="sxs-lookup"><span data-stu-id="33956-180">hello blobs within hello container follow hello same format across Diagnostic Logs and hello Activity Log.</span></span> <span data-ttu-id="33956-181">Эти большие двоичные объекты Hello структура выглядит:</span><span class="sxs-lookup"><span data-stu-id="33956-181">hello structure of these blobs is:</span></span>

> <span data-ttu-id="33956-182">insights-logs-{имя категории журнала}/resourceId=/SUBSCRIPTIONS/{код подписки}/RESOURCEGROUPS/{имя группы ресурсов}/PROVIDERS/{имя поставщика ресурсов}/{тип ресурса}/{имя ресурса}/y={год цифрами, 4 цифры}/m={месяц цифрами, 2 цифры}/d={день цифрами, 2 цифры}/h={время цифрами, 2 цифры, 24-часовой формат}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="33956-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="33956-183">Или даже еще проще:</span><span class="sxs-lookup"><span data-stu-id="33956-183">Or, more simply,</span></span>

> <span data-ttu-id="33956-184">insights-logs-{имя категории журнала}/resourceId=/{resource Id}/y={год цифрами, 4 цифры}/m={месяц цифрами, 2 цифры}/d={день цифрами, 2 цифры}/h={время цифрами, 2 цифры, 24-часовой формат}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="33956-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="33956-185">Например, большой двоичный объект может иметь такое имя:</span><span class="sxs-lookup"><span data-stu-id="33956-185">For example, a blob name might be:</span></span>

> <span data-ttu-id="33956-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="33956-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="33956-187">Каждый BLOB-объект PT1H.json содержит большой двоичный объект JSON, событий, произошедших в течение часа hello, указанный в URL-адрес hello больших двоичных объектов (например, h = 12).</span><span class="sxs-lookup"><span data-stu-id="33956-187">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (for example, h=12).</span></span> <span data-ttu-id="33956-188">Во время hello присутствует час события, добавленных toohello PT1H.json файл, как только они происходят.</span><span class="sxs-lookup"><span data-stu-id="33956-188">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="33956-189">Здравствуйте, значение минуты (m = 00) всегда равно 00, так как события журнала диагностики разбиваются на отдельные большие двоичные объекты в час.</span><span class="sxs-lookup"><span data-stu-id="33956-189">hello minute value (m=00) is always 00, since diagnostic log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="33956-190">В файле PT1H.json hello каждое событие хранится в массиве записей «hello», в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="33956-190">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| <span data-ttu-id="33956-191">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="33956-191">Element name</span></span> | <span data-ttu-id="33956-192">Описание</span><span class="sxs-lookup"><span data-stu-id="33956-192">Description</span></span> |
| --- | --- |
| <span data-ttu-id="33956-193">Twitter в режиме реального</span><span class="sxs-lookup"><span data-stu-id="33956-193">time</span></span> |<span data-ttu-id="33956-194">Отметка времени, когда hello событий, созданных hello hello Azure служба обработки запроса соответствующее событие hello.</span><span class="sxs-lookup"><span data-stu-id="33956-194">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="33956-195">resourceId</span><span class="sxs-lookup"><span data-stu-id="33956-195">resourceId</span></span> |<span data-ttu-id="33956-196">Идентификатор ресурса hello влияния ресурсов.</span><span class="sxs-lookup"><span data-stu-id="33956-196">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="33956-197">operationName</span><span class="sxs-lookup"><span data-stu-id="33956-197">operationName</span></span> |<span data-ttu-id="33956-198">Имя операции hello.</span><span class="sxs-lookup"><span data-stu-id="33956-198">Name of hello operation.</span></span> |
| <span data-ttu-id="33956-199">category</span><span class="sxs-lookup"><span data-stu-id="33956-199">category</span></span> |<span data-ttu-id="33956-200">Категории журнала событий hello.</span><span class="sxs-lookup"><span data-stu-id="33956-200">Log category of hello event.</span></span> |
| <span data-ttu-id="33956-201">properties</span><span class="sxs-lookup"><span data-stu-id="33956-201">properties</span></span> |<span data-ttu-id="33956-202">Набор `<Key, Value>` пары (т. е. словарь), описывающий hello подробных сведениях события hello.</span><span class="sxs-lookup"><span data-stu-id="33956-202">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="33956-203">свойства Hello и использовании этих свойств зависит от ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="33956-203">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="33956-204">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="33956-204">Next steps</span></span>
* [<span data-ttu-id="33956-205">Скачивание больших двоичных объектов для анализа</span><span class="sxs-lookup"><span data-stu-id="33956-205">Download blobs for analysis</span></span>](../storage/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="33956-206">Stream диагностических журналов пространство имен tooan концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="33956-206">Stream diagnostic logs tooan Event Hubs namespace</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="33956-207">Сбор и использование данных журнала из ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="33956-207">Read more about diagnostic logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
