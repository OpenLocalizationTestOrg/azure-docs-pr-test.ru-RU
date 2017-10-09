---
title: "aaaIT соединителя службы управления в OMS | Документы Microsoft"
description: "С помощью монитора toocentrally hello соединителя службы управления службы ИТ управлять hello ITSM рабочими элементами в OMS и устраните все проблемы, быстро."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="d69ca-103">Централизованное управление рабочими элементами ITSM с помощью соединителя управления ИТ-службами (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="d69ca-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Символ соединителя управления ИТ-службами](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="d69ca-105">Можно использовать hello ИТ службы управления соединителя (ITSMC) в мониторе toocentrally аналитики журнала OMS и управлять рабочими элементами через ITSM продуктов и услуг.</span><span class="sxs-lookup"><span data-stu-id="d69ca-105">You can use hello IT Service Management Connector (ITSMC) in OMS Log Analytics toocentrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="d69ca-106">Hello соединителя службы управления службы ИТ интегрирует существующей ИТ службы управления (ITSM)-продуктов и служб с помощью аналитики журналов OMS.</span><span class="sxs-lookup"><span data-stu-id="d69ca-106">hello IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="d69ca-107">Hello решение содержит двунаправленный интеграция с ITSM продуктов и услуг, там, где он предоставляет hello OMS пользователей инцидентов toocreate параметр, предупреждения или события в решении ITSM.</span><span class="sxs-lookup"><span data-stu-id="d69ca-107">hello solution has bidirectional integration with ITSM products/services, where it provides hello OMS users an option toocreate incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="d69ca-108">Hello соединитель импортирует данные, такие как инциденты и из решения ITSM запросы на изменение в аналитику журнала OMS.</span><span class="sxs-lookup"><span data-stu-id="d69ca-108">hello connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="d69ca-109">С помощью соединителя управления ИТ-службами вы можете:</span><span class="sxs-lookup"><span data-stu-id="d69ca-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="d69ca-110">Централизованно отслеживать и администрировать рабочие элементы для продуктов и служб ITSM, используемых вашей организацией.</span><span class="sxs-lookup"><span data-stu-id="d69ca-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="d69ca-111">Создавать рабочие элементы ITSM (например, оповещения, события и инциденты) в ITSM из оповещений OMS или с помощью поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="d69ca-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="d69ca-112">Считывать инциденты и запросы на изменения из решений ITSM и сопоставлять с соответствующими данными журнала в рабочей области Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d69ca-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="d69ca-113">Найти все события непредвиденным и необычные и устраните их, даже перед конечным пользователям hello вызова и сообщать о них toohello службы технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="d69ca-113">Find any unexpected and unusual events and resolve them, even before hello end users call and report them toohello helpdesk.</span></span>
  - <span data-ttu-id="d69ca-114">Импортировать данные рабочих элементов в Log Analytics и создавать отчеты о ключевых показателях эффективности.</span><span class="sxs-lookup"><span data-stu-id="d69ca-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="d69ca-115">С помощью этих отчетов можно выявлять и оценивать несколько важных элементов, например оценка вредоносных программ, и предпринимать действия над ними.</span><span class="sxs-lookup"><span data-stu-id="d69ca-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="d69ca-116">Просматривать выбранные панели мониторинга, чтобы подробнее ознакомиться с инцидентами, запросами на изменения и затронутыми системами.</span><span class="sxs-lookup"><span data-stu-id="d69ca-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="d69ca-117">Устранение неполадок быстрее путем сопоставления с другими решениями для управления в рабочей области аналитики журналов hello.</span><span class="sxs-lookup"><span data-stu-id="d69ca-117">Troubleshoot faster by correlating with other management solutions in hello Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d69ca-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d69ca-118">Prerequisites</span></span>

<span data-ttu-id="d69ca-119">tooimport hello ITSM рабочих элементов в службе анализа журналов OMS, hello решения требуется подключение между hello соединителя службы управления службы ИТ в hello OMS и hello SM ИТ продуктов и служб можно импортировать из hello рабочих элементов.</span><span class="sxs-lookup"><span data-stu-id="d69ca-119">tooimport hello ITSM work items into OMS Log Analytics, hello solution requires a connection between hello IT Service Management Connector in hello OMS and hello IT SM product/service from which you import hello work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="d69ca-120">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="d69ca-120">Configuration</span></span>

<span data-ttu-id="d69ca-121">Добавить hello соединителя службы управления службы ИТ решения tooyour OMS рабочей области с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="d69ca-121">Add hello IT Service Management Connector solution tooyour OMS work space, using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="d69ca-122">Соединитель управления служб ИТ плитку, как видно из коллекции решений hello:</span><span class="sxs-lookup"><span data-stu-id="d69ca-122">IT Service Management Connector tile as you see in hello Solutions gallery:</span></span>

![Плитка соединителя](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="d69ca-124">После успешного. Кроме того, вы увидите hello соединителя службы управления ИТ, в разделе **OMS** > **параметры** > **подключенные источники.**</span><span class="sxs-lookup"><span data-stu-id="d69ca-124">After successful addition, you will see hello IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC подключен](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="d69ca-126">По умолчанию hello соединителя службы управления службы ИТ обновляет данные hello подключения один раз за каждые 24 часа.</span><span class="sxs-lookup"><span data-stu-id="d69ca-126">By default, hello IT Service Management Connector refreshes hello connection's data once in every 24 hours.</span></span> <span data-ttu-id="d69ca-127">toorefresh подключение к мгновенно для изменения ни один шаблон обновления данных, сделать, нажмите кнопку Далее подключение tooyour hello обновления кнопка отображается.</span><span class="sxs-lookup"><span data-stu-id="d69ca-127">toorefresh your connection's data instantly for any edits or template updates that you make, click hello refresh button displayed next tooyour connection.</span></span>

 ![Обновление ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="d69ca-129">Пакеты управления</span><span class="sxs-lookup"><span data-stu-id="d69ca-129">Management packs</span></span>
<span data-ttu-id="d69ca-130">Для этого решения не требуются какие-либо пакеты управления.</span><span class="sxs-lookup"><span data-stu-id="d69ca-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="d69ca-131">Подключенные источники</span><span class="sxs-lookup"><span data-stu-id="d69ca-131">Connected sources</span></span>

<span data-ttu-id="d69ca-132">Hello следующие продукты и услуги ITSM поддерживаются hello ИТ службы управления соединителя:</span><span class="sxs-lookup"><span data-stu-id="d69ca-132">hello following ITSM products/services are supported by hello IT Service Management Connector:</span></span>

- <span data-ttu-id="d69ca-133">[System Center Service Manager](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms);</span><span class="sxs-lookup"><span data-stu-id="d69ca-133">[System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)</span></span>

- [<span data-ttu-id="d69ca-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="d69ca-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- <span data-ttu-id="d69ca-135">[Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms);</span><span class="sxs-lookup"><span data-stu-id="d69ca-135">[Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)</span></span>  

- [<span data-ttu-id="d69ca-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="d69ca-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a><span data-ttu-id="d69ca-137">С помощью решения hello</span><span class="sxs-lookup"><span data-stu-id="d69ca-137">Using hello solution</span></span>

<span data-ttu-id="d69ca-138">После подключения hello соединителя службы управления службы ИТ в OMS с вашей службой ITSM hello службы анализа журналов начинается сбор данных hello hello подключен ITSM продукты или службы.</span><span class="sxs-lookup"><span data-stu-id="d69ca-138">Once you connect hello OMS IT Service Management Connector with your ITSM service, hello Log Analytics services starts gathering hello data from hello connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="d69ca-139">Данные, импортированные соединителем управления ИТ-службами, отображаются в Log Analytics в качестве событий **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="d69ca-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="d69ca-140">Событие содержит поле с именем **ServiceDeskWorkItemType_s**,</span><span class="sxs-lookup"><span data-stu-id="d69ca-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="d69ca-141">который занять его значение как инцидента, или запроса на изменение, в зависимости от hello рабочих элементов данных, содержащихся в hello **ServiceDesk_CL** событий.</span><span class="sxs-lookup"><span data-stu-id="d69ca-141">which can take its value as incident, or change request, depending on hello work item data contained in hello **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="d69ca-142">Входные данные</span><span class="sxs-lookup"><span data-stu-id="d69ca-142">Input data</span></span>
<span data-ttu-id="d69ca-143">Рабочие элементы, импортированные из hello ITSM продуктов и услуг.</span><span class="sxs-lookup"><span data-stu-id="d69ca-143">Work items imported from hello ITSM products/services.</span></span>

<span data-ttu-id="d69ca-144">Hello следующие сведения приведены примеры данные, собранные соединителем ИТ hello.</span><span class="sxs-lookup"><span data-stu-id="d69ca-144">hello following information shows examples of data gathered by hello IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="d69ca-145">В зависимости от hello тип рабочего элемента импортирован в службы анализа журналов, **ServiceDesk_CL** содержит hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="d69ca-145">Depending on hello work item type imported into Log Analytics, **ServiceDesk_CL** contains hello following fields:</span></span>

<span data-ttu-id="d69ca-146">**Рабочий элемент:** **инциденты**</span><span class="sxs-lookup"><span data-stu-id="d69ca-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="d69ca-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="d69ca-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="d69ca-148">**Поля**</span><span class="sxs-lookup"><span data-stu-id="d69ca-148">**Fields**</span></span>

- <span data-ttu-id="d69ca-149">ServiceDeskConnectionName;</span><span class="sxs-lookup"><span data-stu-id="d69ca-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="d69ca-150">"Идентификатор службы поддержки";</span><span class="sxs-lookup"><span data-stu-id="d69ca-150">Service Desk ID</span></span>
- <span data-ttu-id="d69ca-151">Состояние</span><span class="sxs-lookup"><span data-stu-id="d69ca-151">State</span></span>
- <span data-ttu-id="d69ca-152">"Срочность";</span><span class="sxs-lookup"><span data-stu-id="d69ca-152">Urgency</span></span>
- <span data-ttu-id="d69ca-153">Влияние</span><span class="sxs-lookup"><span data-stu-id="d69ca-153">Impact</span></span>
- <span data-ttu-id="d69ca-154">Приоритет</span><span class="sxs-lookup"><span data-stu-id="d69ca-154">Priority</span></span>
- <span data-ttu-id="d69ca-155">Escalation (Эскалация);</span><span class="sxs-lookup"><span data-stu-id="d69ca-155">Escalation</span></span>
- <span data-ttu-id="d69ca-156">"Кем создано";</span><span class="sxs-lookup"><span data-stu-id="d69ca-156">Created By</span></span>
- <span data-ttu-id="d69ca-157">"Кем разрешено";</span><span class="sxs-lookup"><span data-stu-id="d69ca-157">Resolved By</span></span>
- <span data-ttu-id="d69ca-158">Closed By (Кем закрыто);</span><span class="sxs-lookup"><span data-stu-id="d69ca-158">Closed By</span></span>
- <span data-ttu-id="d69ca-159">Источник</span><span class="sxs-lookup"><span data-stu-id="d69ca-159">Source</span></span>
- <span data-ttu-id="d69ca-160">Кому назначено</span><span class="sxs-lookup"><span data-stu-id="d69ca-160">Assigned To</span></span>
- <span data-ttu-id="d69ca-161">Категория</span><span class="sxs-lookup"><span data-stu-id="d69ca-161">Category</span></span>
- <span data-ttu-id="d69ca-162">Название</span><span class="sxs-lookup"><span data-stu-id="d69ca-162">Title</span></span>
- <span data-ttu-id="d69ca-163">Описание</span><span class="sxs-lookup"><span data-stu-id="d69ca-163">Description</span></span>
- <span data-ttu-id="d69ca-164">"Дата создания";</span><span class="sxs-lookup"><span data-stu-id="d69ca-164">Created Date</span></span>
- <span data-ttu-id="d69ca-165">Closed Date (Дата закрытия);</span><span class="sxs-lookup"><span data-stu-id="d69ca-165">Closed Date</span></span>
- <span data-ttu-id="d69ca-166">Resolved Date (Дата разрешения);</span><span class="sxs-lookup"><span data-stu-id="d69ca-166">Resolved Date</span></span>
- <span data-ttu-id="d69ca-167">"Дата последнего изменения";</span><span class="sxs-lookup"><span data-stu-id="d69ca-167">Last Modified Date</span></span>
- <span data-ttu-id="d69ca-168">Компьютер</span><span class="sxs-lookup"><span data-stu-id="d69ca-168">Computer</span></span>


<span data-ttu-id="d69ca-169">**Рабочий элемент:** **запросы на изменение**</span><span class="sxs-lookup"><span data-stu-id="d69ca-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="d69ca-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="d69ca-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="d69ca-171">**Поля**</span><span class="sxs-lookup"><span data-stu-id="d69ca-171">**Fields**</span></span>
- <span data-ttu-id="d69ca-172">ServiceDeskConnectionName;</span><span class="sxs-lookup"><span data-stu-id="d69ca-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="d69ca-173">"Идентификатор службы поддержки";</span><span class="sxs-lookup"><span data-stu-id="d69ca-173">Service Desk ID</span></span>
- <span data-ttu-id="d69ca-174">"Кем создано";</span><span class="sxs-lookup"><span data-stu-id="d69ca-174">Created By</span></span>
- <span data-ttu-id="d69ca-175">Closed By (Кем закрыто);</span><span class="sxs-lookup"><span data-stu-id="d69ca-175">Closed By</span></span>
- <span data-ttu-id="d69ca-176">Источник</span><span class="sxs-lookup"><span data-stu-id="d69ca-176">Source</span></span>
- <span data-ttu-id="d69ca-177">Кому назначено</span><span class="sxs-lookup"><span data-stu-id="d69ca-177">Assigned To</span></span>
- <span data-ttu-id="d69ca-178">Название</span><span class="sxs-lookup"><span data-stu-id="d69ca-178">Title</span></span>
- <span data-ttu-id="d69ca-179">Тип</span><span class="sxs-lookup"><span data-stu-id="d69ca-179">Type</span></span>
- <span data-ttu-id="d69ca-180">Категория</span><span class="sxs-lookup"><span data-stu-id="d69ca-180">Category</span></span>
- <span data-ttu-id="d69ca-181">Состояние</span><span class="sxs-lookup"><span data-stu-id="d69ca-181">State</span></span>
- <span data-ttu-id="d69ca-182">Escalation (Эскалация);</span><span class="sxs-lookup"><span data-stu-id="d69ca-182">Escalation</span></span>
- <span data-ttu-id="d69ca-183">Conflict Status (Состояние конфликта);</span><span class="sxs-lookup"><span data-stu-id="d69ca-183">Conflict Status</span></span>
- <span data-ttu-id="d69ca-184">"Срочность";</span><span class="sxs-lookup"><span data-stu-id="d69ca-184">Urgency</span></span>
- <span data-ttu-id="d69ca-185">Приоритет</span><span class="sxs-lookup"><span data-stu-id="d69ca-185">Priority</span></span>
- <span data-ttu-id="d69ca-186">"Риск";</span><span class="sxs-lookup"><span data-stu-id="d69ca-186">Risk</span></span>
- <span data-ttu-id="d69ca-187">Влияние</span><span class="sxs-lookup"><span data-stu-id="d69ca-187">Impact</span></span>
- <span data-ttu-id="d69ca-188">Кому назначено</span><span class="sxs-lookup"><span data-stu-id="d69ca-188">Assigned To</span></span>
- <span data-ttu-id="d69ca-189">"Дата создания";</span><span class="sxs-lookup"><span data-stu-id="d69ca-189">Created Date</span></span>
- <span data-ttu-id="d69ca-190">Closed Date (Дата закрытия);</span><span class="sxs-lookup"><span data-stu-id="d69ca-190">Closed Date</span></span>
- <span data-ttu-id="d69ca-191">"Дата последнего изменения";</span><span class="sxs-lookup"><span data-stu-id="d69ca-191">Last Modified Date</span></span>
- <span data-ttu-id="d69ca-192">Requested Date (Запрошенная дата);</span><span class="sxs-lookup"><span data-stu-id="d69ca-192">Requested Date</span></span>
- <span data-ttu-id="d69ca-193">Planned Start Date (Планируемая дата начала);</span><span class="sxs-lookup"><span data-stu-id="d69ca-193">Planned Start Date</span></span>
- <span data-ttu-id="d69ca-194">Planned End Date (Планируемая дата окончания);</span><span class="sxs-lookup"><span data-stu-id="d69ca-194">Planned End Date</span></span>
- <span data-ttu-id="d69ca-195">Work Start Date (Дата начала работы);</span><span class="sxs-lookup"><span data-stu-id="d69ca-195">Work Start Date</span></span>
- <span data-ttu-id="d69ca-196">Work End Date (Дата окончания работы);</span><span class="sxs-lookup"><span data-stu-id="d69ca-196">Work End Date</span></span>
- <span data-ttu-id="d69ca-197">Описание</span><span class="sxs-lookup"><span data-stu-id="d69ca-197">Description</span></span>
- <span data-ttu-id="d69ca-198">Компьютер</span><span class="sxs-lookup"><span data-stu-id="d69ca-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="d69ca-199">Выходные данные инцидента ServiceNow</span><span class="sxs-lookup"><span data-stu-id="d69ca-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="d69ca-200">Поле OMS</span><span class="sxs-lookup"><span data-stu-id="d69ca-200">OMS field</span></span> | <span data-ttu-id="d69ca-201">Поле ITSM</span><span class="sxs-lookup"><span data-stu-id="d69ca-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="d69ca-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-202">ServiceDeskId_s</span></span>| <span data-ttu-id="d69ca-203">Number</span><span class="sxs-lookup"><span data-stu-id="d69ca-203">Number</span></span> |
| <span data-ttu-id="d69ca-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-204">IncidentState_s</span></span> | <span data-ttu-id="d69ca-205">Состояние</span><span class="sxs-lookup"><span data-stu-id="d69ca-205">State</span></span> |
| <span data-ttu-id="d69ca-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-206">Urgency_s</span></span> |<span data-ttu-id="d69ca-207">"Срочность";</span><span class="sxs-lookup"><span data-stu-id="d69ca-207">Urgency</span></span> |
| <span data-ttu-id="d69ca-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-208">Impact_s</span></span> |<span data-ttu-id="d69ca-209">Влияние</span><span class="sxs-lookup"><span data-stu-id="d69ca-209">Impact</span></span>|
| <span data-ttu-id="d69ca-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-210">Priority_s</span></span> | <span data-ttu-id="d69ca-211">Приоритет</span><span class="sxs-lookup"><span data-stu-id="d69ca-211">Priority</span></span> |
| <span data-ttu-id="d69ca-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-212">CreatedBy_s</span></span> | <span data-ttu-id="d69ca-213">Opened by (Кем открыто)</span><span class="sxs-lookup"><span data-stu-id="d69ca-213">Opened by</span></span> |
| <span data-ttu-id="d69ca-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-214">ResolvedBy_s</span></span> | <span data-ttu-id="d69ca-215">"Кем разрешено"</span><span class="sxs-lookup"><span data-stu-id="d69ca-215">Resolved by</span></span>|
| <span data-ttu-id="d69ca-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-216">ClosedBy_s</span></span>  | <span data-ttu-id="d69ca-217">Closed By (Кем закрыто)</span><span class="sxs-lookup"><span data-stu-id="d69ca-217">Closed by</span></span> |
| <span data-ttu-id="d69ca-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-218">Source_s</span></span>| <span data-ttu-id="d69ca-219">Contact type (Тип контакта)</span><span class="sxs-lookup"><span data-stu-id="d69ca-219">Contact type</span></span> |
| <span data-ttu-id="d69ca-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-220">AssignedTo_s</span></span> | <span data-ttu-id="d69ca-221">Назначенный слишком</span><span class="sxs-lookup"><span data-stu-id="d69ca-221">Assigned too</span></span> |
| <span data-ttu-id="d69ca-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-222">Category_s</span></span> | <span data-ttu-id="d69ca-223">Категория</span><span class="sxs-lookup"><span data-stu-id="d69ca-223">Category</span></span> |
| <span data-ttu-id="d69ca-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-224">Title_s</span></span>|  <span data-ttu-id="d69ca-225">Краткое описание</span><span class="sxs-lookup"><span data-stu-id="d69ca-225">Short description</span></span> |
| <span data-ttu-id="d69ca-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-226">Description_s</span></span>|  <span data-ttu-id="d69ca-227">Примечания</span><span class="sxs-lookup"><span data-stu-id="d69ca-227">Notes</span></span> |
| <span data-ttu-id="d69ca-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="d69ca-228">CreatedDate_t</span></span>|  <span data-ttu-id="d69ca-229">Opened (Открыто)</span><span class="sxs-lookup"><span data-stu-id="d69ca-229">Opened</span></span> |
| <span data-ttu-id="d69ca-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="d69ca-230">ClosedDate_t</span></span>| <span data-ttu-id="d69ca-231">closed</span><span class="sxs-lookup"><span data-stu-id="d69ca-231">closed</span></span>|
| <span data-ttu-id="d69ca-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="d69ca-232">ResolvedDate_t</span></span>|<span data-ttu-id="d69ca-233">"Разрешено"</span><span class="sxs-lookup"><span data-stu-id="d69ca-233">Resolved</span></span>|
| <span data-ttu-id="d69ca-234">Компьютер</span><span class="sxs-lookup"><span data-stu-id="d69ca-234">Computer</span></span>  | <span data-ttu-id="d69ca-235">Элемент конфигурации</span><span class="sxs-lookup"><span data-stu-id="d69ca-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="d69ca-236">Выходные данные запроса на изменение ServiceNow</span><span class="sxs-lookup"><span data-stu-id="d69ca-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="d69ca-237">Поле OMS</span><span class="sxs-lookup"><span data-stu-id="d69ca-237">OMS field</span></span> | <span data-ttu-id="d69ca-238">Поле ITSM</span><span class="sxs-lookup"><span data-stu-id="d69ca-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="d69ca-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-239">ServiceDeskId_s</span></span>| <span data-ttu-id="d69ca-240">Number</span><span class="sxs-lookup"><span data-stu-id="d69ca-240">Number</span></span> |
| <span data-ttu-id="d69ca-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-241">CreatedBy_s</span></span> | <span data-ttu-id="d69ca-242">"Кем запрошено"</span><span class="sxs-lookup"><span data-stu-id="d69ca-242">Requested by</span></span> |
| <span data-ttu-id="d69ca-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-243">ClosedBy_s</span></span> | <span data-ttu-id="d69ca-244">Closed By (Кем закрыто)</span><span class="sxs-lookup"><span data-stu-id="d69ca-244">Closed by</span></span> |
| <span data-ttu-id="d69ca-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-245">AssignedTo_s</span></span> | <span data-ttu-id="d69ca-246">Назначенный слишком</span><span class="sxs-lookup"><span data-stu-id="d69ca-246">Assigned too</span></span> |
| <span data-ttu-id="d69ca-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-247">Title_s</span></span>|  <span data-ttu-id="d69ca-248">Краткое описание</span><span class="sxs-lookup"><span data-stu-id="d69ca-248">Short description</span></span> |
| <span data-ttu-id="d69ca-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-249">Type_s</span></span>|  <span data-ttu-id="d69ca-250">Тип</span><span class="sxs-lookup"><span data-stu-id="d69ca-250">Type</span></span> |
| <span data-ttu-id="d69ca-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-251">Category_s</span></span>|  <span data-ttu-id="d69ca-252">Catgory</span><span class="sxs-lookup"><span data-stu-id="d69ca-252">Catgory</span></span> |
| <span data-ttu-id="d69ca-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-253">CRState_s</span></span>|  <span data-ttu-id="d69ca-254">Состояние</span><span class="sxs-lookup"><span data-stu-id="d69ca-254">State</span></span>|
| <span data-ttu-id="d69ca-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-255">Urgency_s</span></span>|  <span data-ttu-id="d69ca-256">"Срочность";</span><span class="sxs-lookup"><span data-stu-id="d69ca-256">Urgency</span></span> |
| <span data-ttu-id="d69ca-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-257">Priority_s</span></span>| <span data-ttu-id="d69ca-258">Приоритет</span><span class="sxs-lookup"><span data-stu-id="d69ca-258">Priority</span></span>|
| <span data-ttu-id="d69ca-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-259">Risk_s</span></span>| <span data-ttu-id="d69ca-260">"Риск";</span><span class="sxs-lookup"><span data-stu-id="d69ca-260">Risk</span></span>|
| <span data-ttu-id="d69ca-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-261">Impact_s</span></span>| <span data-ttu-id="d69ca-262">Влияние</span><span class="sxs-lookup"><span data-stu-id="d69ca-262">Impact</span></span>|
| <span data-ttu-id="d69ca-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="d69ca-263">RequestedDate_t</span></span>  | <span data-ttu-id="d69ca-264">Requested by date</span><span class="sxs-lookup"><span data-stu-id="d69ca-264">Requested by date</span></span> |
| <span data-ttu-id="d69ca-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="d69ca-265">ClosedDate_t</span></span> | <span data-ttu-id="d69ca-266">Closed Date (Дата закрытия)</span><span class="sxs-lookup"><span data-stu-id="d69ca-266">Closed date</span></span> |
| <span data-ttu-id="d69ca-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="d69ca-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="d69ca-268">Planned Start Date (Планируемая дата начала)</span><span class="sxs-lookup"><span data-stu-id="d69ca-268">Planned start date</span></span> |
| <span data-ttu-id="d69ca-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="d69ca-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="d69ca-270">Planned End Date (Планируемая дата окончания)</span><span class="sxs-lookup"><span data-stu-id="d69ca-270">Planned end date</span></span> |
| <span data-ttu-id="d69ca-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="d69ca-271">WorkStartDate_t</span></span>  | <span data-ttu-id="d69ca-272">Actual start date (Фактическая дата начала)</span><span class="sxs-lookup"><span data-stu-id="d69ca-272">Actual start date</span></span> |
| <span data-ttu-id="d69ca-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="d69ca-273">WorkEndDate_t</span></span> | <span data-ttu-id="d69ca-274">Actual end date (Фактическая дата окончания)</span><span class="sxs-lookup"><span data-stu-id="d69ca-274">Actual end date</span></span>|
| <span data-ttu-id="d69ca-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="d69ca-275">Description_s</span></span> | <span data-ttu-id="d69ca-276">Описание</span><span class="sxs-lookup"><span data-stu-id="d69ca-276">Description</span></span> |
| <span data-ttu-id="d69ca-277">Компьютер</span><span class="sxs-lookup"><span data-stu-id="d69ca-277">Computer</span></span>  | <span data-ttu-id="d69ca-278">Элемент конфигурации</span><span class="sxs-lookup"><span data-stu-id="d69ca-278">Configuration Item</span></span> |

<span data-ttu-id="d69ca-279">**Снимок экрана с примером Log Analytics для данных ITSM:**</span><span class="sxs-lookup"><span data-stu-id="d69ca-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Снимок экрана с Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="d69ca-281">Интеграция соединителя управления ИТ-службами с другими решениями OMS</span><span class="sxs-lookup"><span data-stu-id="d69ca-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="d69ca-282">Соединитель управления ИТ-служб, в настоящее время поддерживает интеграцию с hello карту службы решения.</span><span class="sxs-lookup"><span data-stu-id="d69ca-282">IT Service Management Connector, currently supports integration with hello Service Map solution.</span></span>

<span data-ttu-id="d69ca-283">Схемы услуг автоматически обнаруживает hello компонентов приложений в Windows и системами Linux и карты hello обмен данными между службами.</span><span class="sxs-lookup"><span data-stu-id="d69ca-283">Service Map automatically discovers hello application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="d69ca-284">Она позволяет tooview серверов как можно считать из них — взаимосвязанных систем, доставляющих критически важных служб.</span><span class="sxs-lookup"><span data-stu-id="d69ca-284">It allows you tooview your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="d69ca-285">Схема услуги отображает сведения о подключениях между серверами, процессами и портами в любой подключенной по протоколу TCP архитектуре без дополнительной настройки. Пользователям требуется только установить агент.</span><span class="sxs-lookup"><span data-stu-id="d69ca-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="d69ca-286">Дополнительные сведения см. в статье [Использование решения схемы услуги в Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="d69ca-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="d69ca-287">Эта интеграция позволяет просматривать элементы поддержки службы hello, созданного в решениях ITSM hello, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="d69ca-287">With this integration, you can view hello service desk items created in hello ITSM solutions as shown in hello following example:</span></span>

![<span data-ttu-id="d69ca-288">Интегрированное решение</span><span class="sxs-lookup"><span data-stu-id="d69ca-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="d69ca-289">Создание рабочих элементов ITSM для оповещений OMS</span><span class="sxs-lookup"><span data-stu-id="d69ca-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="d69ca-290">Для оповещений OMS hello можно создать связанные рабочие элементы в источниках ITSM hello подключен.</span><span class="sxs-lookup"><span data-stu-id="d69ca-290">For hello OMS alerts, you can create associated work items in hello connected ITSM sources.</span></span>  <span data-ttu-id="d69ca-291">toodo, hello используйте следующие процедуры:</span><span class="sxs-lookup"><span data-stu-id="d69ca-291">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="d69ca-292">Из **поиска журналов** выполните данные tooview запросов поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="d69ca-292">From **Log Search** window, run a log search query tooview data.</span></span> <span data-ttu-id="d69ca-293">Результаты запроса являются источником hello для рабочих элементов.</span><span class="sxs-lookup"><span data-stu-id="d69ca-293">Query results are hello source for work items.</span></span>
2. <span data-ttu-id="d69ca-294">В **поиска журналов**, нажмите кнопку **предупреждения** tooopen hello **добавить правило оповещения** страницы.</span><span class="sxs-lookup"><span data-stu-id="d69ca-294">In **Log Search**, click **Alert** tooopen hello **Add Alert Rule** page.</span></span>

    ![Снимок экрана с Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="d69ca-296">На hello **добавить правило оповещения** окна, указать сведения, необходимые hello **имя**, **серьезность**, **поискового запроса**, и  **Предупреждения условий** (окно-метрики времени измерения).</span><span class="sxs-lookup"><span data-stu-id="d69ca-296">On hello **Add Alert Rule** window, provide hello required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="d69ca-297">Для **Действия: ITSM** выберите значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="d69ca-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="d69ca-298">Выберите подключение к ITSM hello **выбрать подключение к** списка.</span><span class="sxs-lookup"><span data-stu-id="d69ca-298">Select your ITSM connection from hello **Select Connection** list.</span></span>
6. <span data-ttu-id="d69ca-299">При необходимости, где подробно hello.</span><span class="sxs-lookup"><span data-stu-id="d69ca-299">Provide hello details as required.</span></span>
7. <span data-ttu-id="d69ca-300">отдельный рабочий элемент для каждой записи журнала из этого предупреждения, выберите hello toocreate **создать отдельные рабочие элементы для каждой записи журнала** флажок.</span><span class="sxs-lookup"><span data-stu-id="d69ca-300">toocreate a separate work item for each log entry of this alert, select hello **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="d69ca-301">Или</span><span class="sxs-lookup"><span data-stu-id="d69ca-301">Or</span></span>

    <span data-ttu-id="d69ca-302">Оставьте этот флажок невыбранные toocreate только один рабочий элемент для любого количества записей журнала в одно оповещение.</span><span class="sxs-lookup"><span data-stu-id="d69ca-302">leave this checkbox unselected toocreate only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="d69ca-303">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d69ca-303">Click **Save**.</span></span>

<span data-ttu-id="d69ca-304">оповещения OMS Hello создаются в папке **предупреждения**.</span><span class="sxs-lookup"><span data-stu-id="d69ca-304">hello OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="d69ca-305">Здравствуйте, соответствующие соединения ITSM рабочие элементы создаются, когда условие hello указанного предупреждения.</span><span class="sxs-lookup"><span data-stu-id="d69ca-305">hello corresponding ITSM connection's work items are created when hello specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="d69ca-306">Создание рабочих элементов ITSM из журналов OMS</span><span class="sxs-lookup"><span data-stu-id="d69ca-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="d69ca-307">Рабочие элементы можно создавать в источниках ITSM hello подключены с помощью функции поиска журналов OMS.</span><span class="sxs-lookup"><span data-stu-id="d69ca-307">You can create work items in hello connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="d69ca-308">toodo, hello используйте следующие процедуры:</span><span class="sxs-lookup"><span data-stu-id="d69ca-308">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="d69ca-309">Из **поиска журналов**, выполнять поиск данных требуется hello, выберите Подробности hello и нажмите кнопку **создать рабочий элемент**.</span><span class="sxs-lookup"><span data-stu-id="d69ca-309">From **Log Search**,  search hello required data, select hello detail, and click **Create work item**.</span></span>

    <span data-ttu-id="d69ca-310">Hello **создать ITSM рабочий элемент** появится окно:</span><span class="sxs-lookup"><span data-stu-id="d69ca-310">hello **Create ITSM Work item** window appears:</span></span>

    ![Снимок экрана с Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="d69ca-312">Добавьте hello, приведенные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="d69ca-312">Add hello following details:</span></span>

  - <span data-ttu-id="d69ca-313">**Заголовок рабочего элемента**: название рабочего элемента hello.</span><span class="sxs-lookup"><span data-stu-id="d69ca-313">**Work item Title**: Title for hello work item.</span></span>
  - <span data-ttu-id="d69ca-314">**Описание операции**: описание для нового рабочего элемента hello.</span><span class="sxs-lookup"><span data-stu-id="d69ca-314">**Work item Description**: Description for hello new work item.</span></span>
  - <span data-ttu-id="d69ca-315">**Затронутые компьютера**: имя компьютера hello, где эти данные журнала был найден.</span><span class="sxs-lookup"><span data-stu-id="d69ca-315">**Affected Computer**: Name of hello computer where this log data was found.</span></span>
  - <span data-ttu-id="d69ca-316">**Выберите подключение**: ITSM подключение, в котором требуется toocreate этот рабочий элемент.</span><span class="sxs-lookup"><span data-stu-id="d69ca-316">**Select Connection**:  ITSM connection in which you want toocreate this work item.</span></span>
  - <span data-ttu-id="d69ca-317">**Рабочий элемент.** Тип рабочего элемента.</span><span class="sxs-lookup"><span data-stu-id="d69ca-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="d69ca-318">toouse существующего шаблона рабочего элемента инцидента, щелкните **Да** под **создать рабочий элемент на основе hello шаблона** и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="d69ca-318">toouse an existing work item template for an incident, click **Yes** under **Generate work item based on hello template** option and then click **Create**.</span></span>

    <span data-ttu-id="d69ca-319">или</span><span class="sxs-lookup"><span data-stu-id="d69ca-319">Or,</span></span>

    <span data-ttu-id="d69ca-320">Нажмите кнопку **нет** Если tooprovide настроенные значения.</span><span class="sxs-lookup"><span data-stu-id="d69ca-320">Click **No** if you want tooprovide your customized values.</span></span>

4. <span data-ttu-id="d69ca-321">Предоставьте соответствующие значения hello в hello **тип контакта**, **влияние**, **срочность**, **категории**, и **подкатегории**  текстовые поля и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="d69ca-321">Provide hello appropriate values in hello **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="d69ca-322">Hello рабочий элемент создается в hello ITSM, который также можно просмотреть в OMS.</span><span class="sxs-lookup"><span data-stu-id="d69ca-322">hello work item will be created in hello ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="d69ca-323">Устранение неполадок с подключением ITSM в OMS</span><span class="sxs-lookup"><span data-stu-id="d69ca-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="d69ca-324">Если происходит сбой подключения из подключенного источника пользовательского интерфейса и получить hello **ошибка при сохранении подключения** сообщение, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d69ca-324">If connection fails from connected source's UI and you get hello **Error in saving connection** message, do hello following:</span></span>
 - <span data-ttu-id="d69ca-325">В случае подключения ServiceNow, Cherwell и Provance убедитесь, что hello правильно введенное имя пользователя и пароль и клиентами идентификатор и секрет клиента для каждого подключения hello.</span><span class="sxs-lookup"><span data-stu-id="d69ca-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  hello username/password and  client ID/client secret  for each of hello connections.</span></span> <span data-ttu-id="d69ca-326">Если hello ошибка будет повторяться, проверьте наличие необходимых прав доступа в hello соответствующие ITSM продукта toomake hello соединения.</span><span class="sxs-lookup"><span data-stu-id="d69ca-326">If hello error persists, check if you have sufficient privileges  in hello corresponding ITSM product toomake hello connection.</span></span>
 - <span data-ttu-id="d69ca-327">В случае Service Manager убедитесь, что веб-приложение hello успешно развернут и гибридное подключение создается.</span><span class="sxs-lookup"><span data-stu-id="d69ca-327">In case of Service Manager, ensure that hello Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="d69ca-328">tooverify hello подключение успешно установлено hello на локальном компьютере Service Manager, посетите hello URL-адрес приложения как описано в документации hello для создания hello [гибридного подключения](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="d69ca-328">tooverify hello connection is successfully established with hello on-prem Service Manager machine, visit hello  Web app URL as detailed in hello documentation for making hello [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="d69ca-329">Если данные из ServiceNow начало синхронизирован не в OMS, убедитесь, что этот экземпляр ServiceNow hello не находится в спящем режиме.</span><span class="sxs-lookup"><span data-stu-id="d69ca-329">If data from ServiceNow is not getting synced in OMS, ensure that hello ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="d69ca-330">Такое некоторое время возможно в hello разработки ServiceNow экземпляры, при ожидании.</span><span class="sxs-lookup"><span data-stu-id="d69ca-330">This might sometime happen in hello ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="d69ca-331">Else, проблемы с отчетом hello.</span><span class="sxs-lookup"><span data-stu-id="d69ca-331">Else, report hello issue.</span></span>
3.  <span data-ttu-id="d69ca-332">Если оповещения, получение срабатывает OMS, но в продукте ITSM не начало создания рабочих элементов или элементы конфигурации, чтобы получить toowork создан и связанные элементы или все сведения общего характера, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d69ca-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked toowork items or for any generic information, do hello following:</span></span>
 -  <span data-ttu-id="d69ca-333">Решение для соединителя службы управления ИТ на портале OMS может быть используется tooget сводку подключений или рабочих элементов/компьютеров и т. д. Щелкните hello сообщение об ошибке в колонке hello состояния, переходы слишком**поиска журналов** и просмотреть hello соединения, имеющий hello ошибку с помощью сведений о hello в сообщении об ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="d69ca-333">IT Service Management Connector solution in OMS portal could be used tooget a summary of connections/work items/computers etc. Click hello error message in hello status blade, navigate too**Log Search** and view hello connection that has hello error by using hello details in hello error message.</span></span>
 - <span data-ttu-id="d69ca-334">непосредственно hello ошибок и связанные сведения можно просмотреть в hello **поиска журналов** страницу с использованием *тип = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="d69ca-334">you can directly view hello errors/related information in hello **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="d69ca-335">Устранение неполадок развертывания веб-приложения Service Manager</span><span class="sxs-lookup"><span data-stu-id="d69ca-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="d69ca-336">В случае каких-либо осложнений с развертывание веб-приложения, убедитесь, имеются достаточные разрешения в подписке hello упомянутые toocreate и развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d69ca-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in hello subscription mentioned toocreate/deploy resources.</span></span>
2.  <span data-ttu-id="d69ca-337">Если **ссылка на объект не задана tooinstance объекта** появляется сообщение об ошибке при выполнении hello [сценарий](log-analytics-itsmc-service-manager-script.md) убедитесь, что вы ввели допустимые значения в группе **Конфигурация пользователя**раздел.</span><span class="sxs-lookup"><span data-stu-id="d69ca-337">If **Object reference not set tooinstance of an object** error message appears while running hello [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="d69ca-338">Если этого не toocreate пространство имен ретрансляции шины обслуживания, убедитесь, что необходимые hello, что поставщик ресурсов зарегистрирован в подписке hello.</span><span class="sxs-lookup"><span data-stu-id="d69ca-338">If you fail toocreate service bus relay namespace, ensure that hello required resource provider is registered in hello subscription.</span></span> <span data-ttu-id="d69ca-339">Если не зарегистрировано, вручную создайте из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d69ca-339">If not registered, manually create it from hello Azure portal.</span></span> <span data-ttu-id="d69ca-340">Можно также создать его при [создании гибридного подключения hello](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d69ca-340">You can also create it while [creating hello hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from hello Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="d69ca-341">Свяжитесь с нами</span><span class="sxs-lookup"><span data-stu-id="d69ca-341">Contact us</span></span>

<span data-ttu-id="d69ca-342">Для запросов или отзывы о hello соединителя службы управления службы ИТ, обратитесь по адресу [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d69ca-342">For any queries or feedback on hello IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d69ca-343">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d69ca-343">Next steps</span></span>
<span data-ttu-id="d69ca-344">[Добавить продукты и услуги ITSM tooIT соединителя службы управления](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="d69ca-344">[Add ITSM products/services tooIT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
