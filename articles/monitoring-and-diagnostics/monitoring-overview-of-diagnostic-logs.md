---
title: "aaaOverview журналов диагностики Azure | Документы Microsoft"
description: "Что такое Azure журналы диагностики и способы их toounderstand событиями, происходящими в ресурс Azure."
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
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="c496e-103">Сбор и использование данных журнала из ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="c496e-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="c496e-104">Что такое журналы диагностики ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="c496e-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="c496e-105">**Журналы диагностики Azure уровня ресурсов** создаваемых ресурса с журнала предоставляет широкие возможности, часто данные об операции hello этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="c496e-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about hello operation of that resource.</span></span> <span data-ttu-id="c496e-106">Hello содержимое этих журналов зависит от типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="c496e-106">hello content of these logs varies by resource type.</span></span> <span data-ttu-id="c496e-107">Например, счетчики правила группы безопасности сети и аудит Key Vault представляют две категории журналов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c496e-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="c496e-108">Журналы диагностики уровня ресурсов отличаются от hello [журнал действий](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="c496e-108">Resource-level diagnostic logs differ from hello [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="c496e-109">Hello журнал действий позволяет контролировать hello операций, которые были выполнены на ресурсы в подписке с помощью диспетчера ресурсов, например, для создания виртуальной машины или удаление приложения логики.</span><span class="sxs-lookup"><span data-stu-id="c496e-109">hello Activity Log provides insight into hello operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="c496e-110">Hello журнал действий — это журнал уровня подписки.</span><span class="sxs-lookup"><span data-stu-id="c496e-110">hello Activity Log is a subscription-level log.</span></span> <span data-ttu-id="c496e-111">Журналы диагностики уровня ресурса дают представление об операциях, которые были выполнены в рамках этого ресурса, например о получении секрета из Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c496e-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="c496e-112">Журналы диагностики уровня ресурса также отличаются от журналов диагностики уровня гостевой ОС.</span><span class="sxs-lookup"><span data-stu-id="c496e-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="c496e-113">Журналы диагностики гостевой ОС собирает агент, работающий на виртуальной машине или поддерживаемом ресурсе другого типа.</span><span class="sxs-lookup"><span data-stu-id="c496e-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="c496e-114">Журналы диагностики уровня ресурсов требуется данные определенных ресурсов агента и записи между hello платформы Azure, когда журналы диагностики гостевой ОС уровень сбора данных из hello операционной системы и приложений, выполняющихся на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c496e-114">Resource-level diagnostic logs require no agent and capture resource-specific data from hello Azure platform itself, while guest OS-level diagnostic logs capture data from hello operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="c496e-115">Не все ресурсы поддержки нового типа ресурса журналов диагностики, описанные здесь hello.</span><span class="sxs-lookup"><span data-stu-id="c496e-115">Not all resources support hello new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="c496e-116">В этой статье перечислены раздел типы ресурсов поддержки новых журналов диагностики hello уровня ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c496e-116">This article contains a section listing which resource types support hello new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="c496e-117">Журналы диагностики ресурсов и другие типы журналов</span><span class="sxs-lookup"><span data-stu-id="c496e-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="c496e-118">Что можно делать с журналами диагностики уровня ресурса</span><span class="sxs-lookup"><span data-stu-id="c496e-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="c496e-119">Ниже приведены некоторые hello вещей, которые можно сделать с помощью журналов диагностики для ресурса.</span><span class="sxs-lookup"><span data-stu-id="c496e-119">Here are some of hello things you can do with resource diagnostic logs:</span></span>

![Логическое размещение журналов диагностики ресурсов](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="c496e-121">Сохранить их tooa [ **учетной записи хранилища** ](monitoring-archive-diagnostic-logs.md) проверка аудита или вручную.</span><span class="sxs-lookup"><span data-stu-id="c496e-121">Save them tooa [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="c496e-122">Можно указать с помощью времени (в днях) хранения hello **параметров диагностики для ресурса**.</span><span class="sxs-lookup"><span data-stu-id="c496e-122">You can specify hello retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="c496e-123">[Слишком потоковую передачу**концентраторов событий** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) продукты для использования службой сторонних или пользовательских analytics решение, например PowerBI.</span><span class="sxs-lookup"><span data-stu-id="c496e-123">[Stream them too**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="c496e-124">Анализ журналов с помощью [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="c496e-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="c496e-125">Можно использовать учетную запись хранения или пространство имен концентраторов событий, не входящий в hello той же подписке, которые hello одного выпуска журналы.</span><span class="sxs-lookup"><span data-stu-id="c496e-125">You can use a storage account or Event Hubs namespace that is not in hello same subscription as hello one emitting logs.</span></span> <span data-ttu-id="c496e-126">Hello пользователь, настраивающий приветствия должен иметь hello соответствующие RBAC доступа tooboth подписки.</span><span class="sxs-lookup"><span data-stu-id="c496e-126">hello user who configures hello setting must have hello appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="c496e-127">Параметры диагностики ресурсов</span><span class="sxs-lookup"><span data-stu-id="c496e-127">Resource diagnostic settings</span></span>
<span data-ttu-id="c496e-128">Журналы диагностики для всех ресурсов, кроме вычислительных, настраиваются с помощью параметров диагностики ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c496e-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="c496e-129">**Параметры диагностики ресурсов** для управления ресурсами:</span><span class="sxs-lookup"><span data-stu-id="c496e-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="c496e-130">Куда отправляются журналы диагностики ресурсов и метрики (учетная запись хранения, концентраторы событий и/или OMS Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="c496e-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="c496e-131">Какие категории журнала отправляются и следует ли отправлять данные метрики.</span><span class="sxs-lookup"><span data-stu-id="c496e-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="c496e-132">Как долго должны храниться журналы каждой категории в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c496e-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="c496e-133">Срок хранения 0 дней означает, что журналы хранятся неограниченно долго.</span><span class="sxs-lookup"><span data-stu-id="c496e-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="c496e-134">В противном случае — значение hello может быть любое число дней от 1 до 2147483647.</span><span class="sxs-lookup"><span data-stu-id="c496e-134">Otherwise, hello value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="c496e-135">Если заданы политики хранения, но сохранения журналов в учетной записи хранения отключена (например, если только выбраны параметры концентраторов событий или OMS), политики хранения hello не действуют.</span><span class="sxs-lookup"><span data-stu-id="c496e-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), hello retention policies have no effect.</span></span>
    - <span data-ttu-id="c496e-136">Политики хранения, примененных в день, поэтому hello регистрирует конец дня (UTC), с датой hello, что теперь находится за пределами hello политику хранения, удаляются.</span><span class="sxs-lookup"><span data-stu-id="c496e-136">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy are deleted.</span></span> <span data-ttu-id="c496e-137">Например если у вас есть политика хранения продолжительностью в один день, в начале hello сегодня день hello hello журналы из позавчерашнего дня hello, будет удален.</span><span class="sxs-lookup"><span data-stu-id="c496e-137">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span>

<span data-ttu-id="c496e-138">Эти параметры настраиваются легко hello параметров диагностики для ресурса в hello портал Azure, посредством команд Azure PowerShell и интерфейс командной строки или с помощью hello [API REST Azure монитор](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="c496e-138">These settings are easily configured via hello diagnostic settings for a resource in hello Azure portal, via Azure PowerShell and CLI commands, or via hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="c496e-139">Журналы диагностики и метрики для hello гостевой ОС уровня использования вычислительных ресурсов (например, виртуальные машины или Service Fabric) [отдельным механизмом для конфигурации и выбора выходов](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="c496e-139">Diagnostic logs and metrics for from hello guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="c496e-140">Как tooenable сбора диагностических журналов ресурсов</span><span class="sxs-lookup"><span data-stu-id="c496e-140">How tooenable collection of resource diagnostic logs</span></span>
<span data-ttu-id="c496e-141">Сбор журналов диагностики ресурсов можно включить [при создании ресурса шаблона диспетчера ресурсов](./monitoring-enable-diagnostic-logs-using-template.md) или после создания ресурса из этого ресурса страницу портала hello.</span><span class="sxs-lookup"><span data-stu-id="c496e-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in hello portal.</span></span> <span data-ttu-id="c496e-142">Можно также включить коллекции в любой момент с помощью команд Azure PowerShell или интерфейс командной строки или с помощью API REST Azure монитор hello.</span><span class="sxs-lookup"><span data-stu-id="c496e-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using hello Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="c496e-143">Эти инструкции могут не относиться непосредственно tooevery ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c496e-143">These instructions may not apply directly tooevery resource.</span></span> <span data-ttu-id="c496e-144">Просмотрите ссылки схемы hello hello нижней части этой страницы toounderstand шаги, которые могут относиться toocertain типов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c496e-144">See hello schema links at hello bottom of this page toounderstand special steps that may apply toocertain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a><span data-ttu-id="c496e-145">Включить сбор журналов диагностики ресурсов на портале hello</span><span class="sxs-lookup"><span data-stu-id="c496e-145">Enable collection of resource diagnostic logs in hello portal</span></span>
<span data-ttu-id="c496e-146">Можно включить сбор журналов диагностики ресурсов в hello Azure портал после создания ресурса будет tooa конкретный ресурс или путем перемещения tooAzure монитора.</span><span class="sxs-lookup"><span data-stu-id="c496e-146">You can enable collection of resource diagnostic logs in hello Azure portal after a resource has been created either by going tooa specific resource or by navigating tooAzure Monitor.</span></span> <span data-ttu-id="c496e-147">tooenable это через монитор Azure:</span><span class="sxs-lookup"><span data-stu-id="c496e-147">tooenable this via Azure Monitor:</span></span>

1. <span data-ttu-id="c496e-148">В hello [портал Azure](http://portal.azure.com)tooAzure монитора перейдите и выберите команду **параметров диагностики**</span><span class="sxs-lookup"><span data-stu-id="c496e-148">In hello [Azure portal](http://portal.azure.com), navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Раздел мониторинга Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="c496e-150">При необходимости фильтровать список hello по группе ресурсов или тип ресурса, а затем щелкните hello ресурсов, для которого вы хотите tooset параметра диагностики.</span><span class="sxs-lookup"><span data-stu-id="c496e-150">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="c496e-151">Если параметры не существует в hello ресурс, который вы выбрали, не запрошенные toocreate параметр.</span><span class="sxs-lookup"><span data-stu-id="c496e-151">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="c496e-152">Щелкните Turn on diagnostics (Включить диагностику).</span><span class="sxs-lookup"><span data-stu-id="c496e-152">Click "Turn on diagnostics."</span></span>

   ![Добавление параметра диагностики — имеющиеся параметры отсутствуют](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="c496e-154">Если имеются существующие параметры ресурсов hello, вы увидите список параметров, уже настроен на этом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="c496e-154">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="c496e-155">Нажмите Add diagnostic setting (Добавить параметр диагностики).</span><span class="sxs-lookup"><span data-stu-id="c496e-155">Click "Add diagnostic setting."</span></span>

   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="c496e-157">Задайте имя параметра, флажки hello для каждого назначения toowhich бы как toosend данные и настройки ресурса, который используется для каждого назначения.</span><span class="sxs-lookup"><span data-stu-id="c496e-157">Give your setting a name, check hello boxes for each destination toowhich you would like toosend data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="c496e-158">При необходимости задайте количество дней tooretain эти журналы с помощью hello **хранения (в днях)** ползунки (только применимые toohello учетной записи местом назначения хранилища).</span><span class="sxs-lookup"><span data-stu-id="c496e-158">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders (only applicable toohello storage account destination).</span></span> <span data-ttu-id="c496e-159">Хранение 0 дней хранит журналы hello бесконечно.</span><span class="sxs-lookup"><span data-stu-id="c496e-159">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="c496e-161">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c496e-161">Click **Save**.</span></span>

<span data-ttu-id="c496e-162">Через несколько секунд hello новый параметр отображается в списке параметров для этого ресурса, а также журналы диагностики отправляются toohello указан назначения сразу созданы новые данные события.</span><span class="sxs-lookup"><span data-stu-id="c496e-162">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are sent toohello specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="c496e-163">Включение сбора журналов диагностики ресурсов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c496e-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="c496e-164">Коллекция tooenable журналы диагностики ресурсов через Azure PowerShell, hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c496e-164">tooenable collection of resource diagnostic logs via Azure PowerShell, use hello following commands:</span></span>

<span data-ttu-id="c496e-165">хранение tooenable в журналах диагностики в учетную запись хранилища, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c496e-165">tooenable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="c496e-166">Идентификатор учетной записи хранилища Hello hello идентификатор ресурса для журналов toowhich учетной записи хранилища hello, требуется toosend hello.</span><span class="sxs-lookup"><span data-stu-id="c496e-166">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="c496e-167">Потоковая передача tooenable концентратора событий tooan журналы диагностики, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c496e-167">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="c496e-168">ИД правила Hello service bus представляет собой строку следующего формата: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="c496e-168">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="c496e-169">tooenable отправки журналов диагностики рабочей области аналитики журналов tooa, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c496e-169">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

<span data-ttu-id="c496e-170">Вы можете получить идентификатор ресурса hello рабочей области аналитики журналов с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c496e-170">You can obtain hello resource ID of your Log Analytics workspace using hello following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="c496e-171">Эти параметры tooenable можно объединить несколько параметров вывода.</span><span class="sxs-lookup"><span data-stu-id="c496e-171">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="c496e-172">Включение сбора журналов диагностики ресурсов с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="c496e-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="c496e-173">Коллекция tooenable журналы диагностики ресурсов через hello Azure CLI, используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c496e-173">tooenable collection of resource diagnostic logs via hello Azure CLI, use hello following commands:</span></span>

<span data-ttu-id="c496e-174">хранение tooenable в журналах диагностики в учетную запись хранилища, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c496e-174">tooenable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="c496e-175">Идентификатор учетной записи хранилища Hello hello идентификатор ресурса для журналов toowhich учетной записи хранилища hello, требуется toosend hello.</span><span class="sxs-lookup"><span data-stu-id="c496e-175">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="c496e-176">Потоковая передача tooenable концентратора событий tooan журналы диагностики, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c496e-176">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="c496e-177">ИД правила Hello service bus представляет собой строку следующего формата: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="c496e-177">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="c496e-178">tooenable отправки журналов диагностики рабочей области аналитики журналов tooa, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c496e-178">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

<span data-ttu-id="c496e-179">Эти параметры tooenable можно объединить несколько параметров вывода.</span><span class="sxs-lookup"><span data-stu-id="c496e-179">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="c496e-180">Включение сбора журналов диагностики ресурсов с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="c496e-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="c496e-181">toochange параметров диагностики с помощью hello Azure REST API-Интерфейс монитора, в разделе [в этом документе](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="c496e-181">toochange diagnostic settings using hello Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a><span data-ttu-id="c496e-182">Управление параметрами диагностических ресурсов в портале hello</span><span class="sxs-lookup"><span data-stu-id="c496e-182">Manage resource diagnostic settings in hello portal</span></span>
<span data-ttu-id="c496e-183">Убедитесь, что все ресурсы настроены с помощью параметров диагностики.</span><span class="sxs-lookup"><span data-stu-id="c496e-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="c496e-184">Перейдите в слишком**монитор** в hello портала и откройте **параметров диагностики**.</span><span class="sxs-lookup"><span data-stu-id="c496e-184">Navigate too**Monitor** in hello portal and open **Diagnostic settings**.</span></span>

![Диагностические журналы колонке hello портала](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="c496e-186">Вы можете иметь tooclick раздел «Дополнительные службы» toofind hello монитора.</span><span class="sxs-lookup"><span data-stu-id="c496e-186">You may have tooclick "More services" toofind hello Monitor section.</span></span>

<span data-ttu-id="c496e-187">Здесь можно просмотреть и отфильтровать все ресурсы, поддерживающие toosee параметров диагностики, если они имеют включении диагностики.</span><span class="sxs-lookup"><span data-stu-id="c496e-187">Here you can view and filter all resources that support diagnostic settings toosee if they have diagnostics enabled.</span></span> <span data-ttu-id="c496e-188">Можно также детализировать toosee, если несколько параметры настроены для ресурса и проверьте какой учетной записи хранилища, пространство имен концентраторов событий и рабочей области аналитики журналов, потоков данных.</span><span class="sxs-lookup"><span data-stu-id="c496e-188">You can also drill down toosee if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Журналы диагностики на портале](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="c496e-190">Добавление параметра диагностики появится представление параметров диагностики, где можно включить, отключить или изменить параметры диагностики для hello hello выбранных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c496e-190">Adding a diagnostic setting brings up hello Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for hello selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="c496e-191">Поддерживаемые службы, категории и схемы для журналов диагностики ресурсов</span><span class="sxs-lookup"><span data-stu-id="c496e-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="c496e-192">[См. в статье](monitoring-diagnostic-logs-schema.md) полный список поддерживаемых служб и категории журнала hello и схем, используемых этими службами.</span><span class="sxs-lookup"><span data-stu-id="c496e-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and hello log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c496e-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c496e-193">Next steps</span></span>

* [<span data-ttu-id="c496e-194">Поток ресурсов журналы диагностики слишком**концентраторов событий**</span><span class="sxs-lookup"><span data-stu-id="c496e-194">Stream resource diagnostic logs too**Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="c496e-195">Изменение параметров диагностики ресурсов, с помощью API REST Azure монитор hello</span><span class="sxs-lookup"><span data-stu-id="c496e-195">Change resource diagnostic settings using hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="c496e-196">Сбор журналов и метрик для служб Azure для использования в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c496e-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
