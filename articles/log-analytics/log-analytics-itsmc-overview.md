---
title: "Соединитель управления ИТ-службами в OMS | Документация Майкрософт"
description: "Использование соединителя управления ИТ-службами для централизованного отслеживания и администрирования рабочих элементов ITSM в OMS, а также для быстрого решения возникающих проблем."
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
ms.openlocfilehash: 54974ef06efdae69ddbfa12b1ba9278b48b113d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="0f67f-103">Централизованное управление рабочими элементами ITSM с помощью соединителя управления ИТ-службами (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="0f67f-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Символ соединителя управления ИТ-службами](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="0f67f-105">Используйте соединитель управления ИТ-службами (ITSMC) в OMS Log Analytics, чтобы централизованно отслеживать и администрировать рабочие элементы между продуктами и службами ITSM.</span><span class="sxs-lookup"><span data-stu-id="0f67f-105">You can use the IT Service Management Connector (ITSMC) in OMS Log Analytics to centrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="0f67f-106">Соединитель управления ИТ-службами интегрирует имеющиеся продукты и службы управления ИТ-службами (ITSM) с OMS Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0f67f-106">The IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="0f67f-107">Решение имеет двунаправленную интеграцию со службами и продуктами ITSM, предоставляя пользователям OMS возможности создавать инциденты, оповещения или события в решении ITSM.</span><span class="sxs-lookup"><span data-stu-id="0f67f-107">The solution has bidirectional integration with ITSM products/services, where it provides the OMS users an option to create incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="0f67f-108">Соединитель также импортирует данные (например, инциденты и запросы на изменения) из решений ITSM в OMS Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0f67f-108">The connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="0f67f-109">С помощью соединителя управления ИТ-службами вы можете:</span><span class="sxs-lookup"><span data-stu-id="0f67f-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="0f67f-110">Централизованно отслеживать и администрировать рабочие элементы для продуктов и служб ITSM, используемых вашей организацией.</span><span class="sxs-lookup"><span data-stu-id="0f67f-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="0f67f-111">Создавать рабочие элементы ITSM (например, оповещения, события и инциденты) в ITSM из оповещений OMS или с помощью поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="0f67f-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="0f67f-112">Считывать инциденты и запросы на изменения из решений ITSM и сопоставлять с соответствующими данными журнала в рабочей области Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0f67f-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="0f67f-113">Находить любые неожиданные и необычные события и устранять связанные с ними проблемы еще до того, как пользователи сообщат о них в службу технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="0f67f-113">Find any unexpected and unusual events and resolve them, even before the end users call and report them to the helpdesk.</span></span>
  - <span data-ttu-id="0f67f-114">Импортировать данные рабочих элементов в Log Analytics и создавать отчеты о ключевых показателях эффективности.</span><span class="sxs-lookup"><span data-stu-id="0f67f-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="0f67f-115">С помощью этих отчетов можно выявлять и оценивать несколько важных элементов, например оценка вредоносных программ, и предпринимать действия над ними.</span><span class="sxs-lookup"><span data-stu-id="0f67f-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="0f67f-116">Просматривать выбранные панели мониторинга, чтобы подробнее ознакомиться с инцидентами, запросами на изменения и затронутыми системами.</span><span class="sxs-lookup"><span data-stu-id="0f67f-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="0f67f-117">Быстро устранять неполадки путем сопоставления с другими решениями по управлению в рабочей области Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0f67f-117">Troubleshoot faster by correlating with other management solutions in the Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0f67f-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0f67f-118">Prerequisites</span></span>

<span data-ttu-id="0f67f-119">Чтобы импортировать рабочие элементы ITSM в OMS Log Analytics, для решения требуется наличие связи между соединителем управления ИТ-службами в OMS и продуктом или службой ITSM, из которой импортируются рабочие элементы.</span><span class="sxs-lookup"><span data-stu-id="0f67f-119">To import the ITSM work items into OMS Log Analytics, the solution requires a connection between the IT Service Management Connector in the OMS and the IT SM product/service from which you import the work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="0f67f-120">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="0f67f-120">Configuration</span></span>

<span data-ttu-id="0f67f-121">Решение "Соединитель управления ИТ-службами" необходимо добавить в рабочую область OMS, как описано в статье [Добавление решений для управления Azure Log Analytics в рабочую область](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="0f67f-121">Add the IT Service Management Connector solution to your OMS work space, using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="0f67f-122">Плитка соединителя управления ИТ-службами в коллекции решений:</span><span class="sxs-lookup"><span data-stu-id="0f67f-122">IT Service Management Connector tile as you see in the Solutions gallery:</span></span>

![Плитка соединителя](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="0f67f-124">После успешного добавления в разделе **OMS** > **Параметры** > **Подключенные источники** отобразится соединитель управления ИТ-службами.</span><span class="sxs-lookup"><span data-stu-id="0f67f-124">After successful addition, you will see the IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC подключен](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="0f67f-126">По умолчанию соединитель управления ИТ-службами обновляет данные подключения каждые 24 часа.</span><span class="sxs-lookup"><span data-stu-id="0f67f-126">By default, the IT Service Management Connector refreshes the connection's data once in every 24 hours.</span></span> <span data-ttu-id="0f67f-127">Чтобы обновить данные после любого изменения или обновления шаблона, нажмите кнопку "Обновить" рядом с подключением.</span><span class="sxs-lookup"><span data-stu-id="0f67f-127">To refresh your connection's data instantly for any edits or template updates that you make, click the refresh button displayed next to your connection.</span></span>

 ![Обновление ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="0f67f-129">Пакеты управления</span><span class="sxs-lookup"><span data-stu-id="0f67f-129">Management packs</span></span>
<span data-ttu-id="0f67f-130">Для этого решения не требуются какие-либо пакеты управления.</span><span class="sxs-lookup"><span data-stu-id="0f67f-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="0f67f-131">Подключенные источники</span><span class="sxs-lookup"><span data-stu-id="0f67f-131">Connected sources</span></span>

<span data-ttu-id="0f67f-132">Соединитель управления ИТ-службами поддерживает следующие службы и продукты ITSM:</span><span class="sxs-lookup"><span data-stu-id="0f67f-132">The following ITSM products/services are supported by the IT Service Management Connector:</span></span>

- <span data-ttu-id="0f67f-133">[System Center Service Manager](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms);</span><span class="sxs-lookup"><span data-stu-id="0f67f-133">[System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)</span></span>

- [<span data-ttu-id="0f67f-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="0f67f-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- <span data-ttu-id="0f67f-135">[Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms);</span><span class="sxs-lookup"><span data-stu-id="0f67f-135">[Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)</span></span>  

- [<span data-ttu-id="0f67f-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="0f67f-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-the-solution"></a><span data-ttu-id="0f67f-137">Использование решения</span><span class="sxs-lookup"><span data-stu-id="0f67f-137">Using the solution</span></span>

<span data-ttu-id="0f67f-138">После подключения соединителя управления ИТ-службами в OMS к службе ITSM службы Log Analytics начинают сбор данных с подключенных продуктов и служб ITSM.</span><span class="sxs-lookup"><span data-stu-id="0f67f-138">Once you connect the OMS IT Service Management Connector with your ITSM service, the Log Analytics services starts gathering the data from the connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="0f67f-139">Данные, импортированные соединителем управления ИТ-службами, отображаются в Log Analytics в качестве событий **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="0f67f-140">Событие содержит поле с именем **ServiceDeskWorkItemType_s**,</span><span class="sxs-lookup"><span data-stu-id="0f67f-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="0f67f-141">которое может принимать значение в качестве инцидента или запроса на изменение в зависимости от данных рабочего элемента, содержащихся в событии **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-141">which can take its value as incident, or change request, depending on the work item data contained in the **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="0f67f-142">Входные данные</span><span class="sxs-lookup"><span data-stu-id="0f67f-142">Input data</span></span>
<span data-ttu-id="0f67f-143">Рабочие элементы импортируются из продуктов и служб ITSM.</span><span class="sxs-lookup"><span data-stu-id="0f67f-143">Work items imported from the ITSM products/services.</span></span>

<span data-ttu-id="0f67f-144">Ниже приведены примеры данных, собранных соединителем управления ИТ-службами.</span><span class="sxs-lookup"><span data-stu-id="0f67f-144">The following information shows examples of data gathered by the IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="0f67f-145">В зависимости от типа рабочего элемента, импортированного в Log Analytics, **ServiceDesk_CL** содержит указанные ниже поля.</span><span class="sxs-lookup"><span data-stu-id="0f67f-145">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="0f67f-146">**Рабочий элемент:** **инциденты**</span><span class="sxs-lookup"><span data-stu-id="0f67f-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="0f67f-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="0f67f-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="0f67f-148">**Поля**</span><span class="sxs-lookup"><span data-stu-id="0f67f-148">**Fields**</span></span>

- <span data-ttu-id="0f67f-149">ServiceDeskConnectionName;</span><span class="sxs-lookup"><span data-stu-id="0f67f-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="0f67f-150">"Идентификатор службы поддержки";</span><span class="sxs-lookup"><span data-stu-id="0f67f-150">Service Desk ID</span></span>
- <span data-ttu-id="0f67f-151">Состояние</span><span class="sxs-lookup"><span data-stu-id="0f67f-151">State</span></span>
- <span data-ttu-id="0f67f-152">"Срочность";</span><span class="sxs-lookup"><span data-stu-id="0f67f-152">Urgency</span></span>
- <span data-ttu-id="0f67f-153">Влияние</span><span class="sxs-lookup"><span data-stu-id="0f67f-153">Impact</span></span>
- <span data-ttu-id="0f67f-154">Приоритет</span><span class="sxs-lookup"><span data-stu-id="0f67f-154">Priority</span></span>
- <span data-ttu-id="0f67f-155">Escalation (Эскалация);</span><span class="sxs-lookup"><span data-stu-id="0f67f-155">Escalation</span></span>
- <span data-ttu-id="0f67f-156">"Кем создано";</span><span class="sxs-lookup"><span data-stu-id="0f67f-156">Created By</span></span>
- <span data-ttu-id="0f67f-157">"Кем разрешено";</span><span class="sxs-lookup"><span data-stu-id="0f67f-157">Resolved By</span></span>
- <span data-ttu-id="0f67f-158">Closed By (Кем закрыто);</span><span class="sxs-lookup"><span data-stu-id="0f67f-158">Closed By</span></span>
- <span data-ttu-id="0f67f-159">Источник</span><span class="sxs-lookup"><span data-stu-id="0f67f-159">Source</span></span>
- <span data-ttu-id="0f67f-160">Кому назначено</span><span class="sxs-lookup"><span data-stu-id="0f67f-160">Assigned To</span></span>
- <span data-ttu-id="0f67f-161">Категория</span><span class="sxs-lookup"><span data-stu-id="0f67f-161">Category</span></span>
- <span data-ttu-id="0f67f-162">Название</span><span class="sxs-lookup"><span data-stu-id="0f67f-162">Title</span></span>
- <span data-ttu-id="0f67f-163">Описание</span><span class="sxs-lookup"><span data-stu-id="0f67f-163">Description</span></span>
- <span data-ttu-id="0f67f-164">"Дата создания";</span><span class="sxs-lookup"><span data-stu-id="0f67f-164">Created Date</span></span>
- <span data-ttu-id="0f67f-165">Closed Date (Дата закрытия);</span><span class="sxs-lookup"><span data-stu-id="0f67f-165">Closed Date</span></span>
- <span data-ttu-id="0f67f-166">Resolved Date (Дата разрешения);</span><span class="sxs-lookup"><span data-stu-id="0f67f-166">Resolved Date</span></span>
- <span data-ttu-id="0f67f-167">"Дата последнего изменения";</span><span class="sxs-lookup"><span data-stu-id="0f67f-167">Last Modified Date</span></span>
- <span data-ttu-id="0f67f-168">Компьютер</span><span class="sxs-lookup"><span data-stu-id="0f67f-168">Computer</span></span>


<span data-ttu-id="0f67f-169">**Рабочий элемент:** **запросы на изменение**</span><span class="sxs-lookup"><span data-stu-id="0f67f-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="0f67f-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="0f67f-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="0f67f-171">**Поля**</span><span class="sxs-lookup"><span data-stu-id="0f67f-171">**Fields**</span></span>
- <span data-ttu-id="0f67f-172">ServiceDeskConnectionName;</span><span class="sxs-lookup"><span data-stu-id="0f67f-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="0f67f-173">"Идентификатор службы поддержки";</span><span class="sxs-lookup"><span data-stu-id="0f67f-173">Service Desk ID</span></span>
- <span data-ttu-id="0f67f-174">"Кем создано";</span><span class="sxs-lookup"><span data-stu-id="0f67f-174">Created By</span></span>
- <span data-ttu-id="0f67f-175">Closed By (Кем закрыто);</span><span class="sxs-lookup"><span data-stu-id="0f67f-175">Closed By</span></span>
- <span data-ttu-id="0f67f-176">Источник</span><span class="sxs-lookup"><span data-stu-id="0f67f-176">Source</span></span>
- <span data-ttu-id="0f67f-177">Кому назначено</span><span class="sxs-lookup"><span data-stu-id="0f67f-177">Assigned To</span></span>
- <span data-ttu-id="0f67f-178">Название</span><span class="sxs-lookup"><span data-stu-id="0f67f-178">Title</span></span>
- <span data-ttu-id="0f67f-179">Тип</span><span class="sxs-lookup"><span data-stu-id="0f67f-179">Type</span></span>
- <span data-ttu-id="0f67f-180">Категория</span><span class="sxs-lookup"><span data-stu-id="0f67f-180">Category</span></span>
- <span data-ttu-id="0f67f-181">Состояние</span><span class="sxs-lookup"><span data-stu-id="0f67f-181">State</span></span>
- <span data-ttu-id="0f67f-182">Escalation (Эскалация);</span><span class="sxs-lookup"><span data-stu-id="0f67f-182">Escalation</span></span>
- <span data-ttu-id="0f67f-183">Conflict Status (Состояние конфликта);</span><span class="sxs-lookup"><span data-stu-id="0f67f-183">Conflict Status</span></span>
- <span data-ttu-id="0f67f-184">"Срочность";</span><span class="sxs-lookup"><span data-stu-id="0f67f-184">Urgency</span></span>
- <span data-ttu-id="0f67f-185">Приоритет</span><span class="sxs-lookup"><span data-stu-id="0f67f-185">Priority</span></span>
- <span data-ttu-id="0f67f-186">"Риск";</span><span class="sxs-lookup"><span data-stu-id="0f67f-186">Risk</span></span>
- <span data-ttu-id="0f67f-187">Влияние</span><span class="sxs-lookup"><span data-stu-id="0f67f-187">Impact</span></span>
- <span data-ttu-id="0f67f-188">Кому назначено</span><span class="sxs-lookup"><span data-stu-id="0f67f-188">Assigned To</span></span>
- <span data-ttu-id="0f67f-189">"Дата создания";</span><span class="sxs-lookup"><span data-stu-id="0f67f-189">Created Date</span></span>
- <span data-ttu-id="0f67f-190">Closed Date (Дата закрытия);</span><span class="sxs-lookup"><span data-stu-id="0f67f-190">Closed Date</span></span>
- <span data-ttu-id="0f67f-191">"Дата последнего изменения";</span><span class="sxs-lookup"><span data-stu-id="0f67f-191">Last Modified Date</span></span>
- <span data-ttu-id="0f67f-192">Requested Date (Запрошенная дата);</span><span class="sxs-lookup"><span data-stu-id="0f67f-192">Requested Date</span></span>
- <span data-ttu-id="0f67f-193">Planned Start Date (Планируемая дата начала);</span><span class="sxs-lookup"><span data-stu-id="0f67f-193">Planned Start Date</span></span>
- <span data-ttu-id="0f67f-194">Planned End Date (Планируемая дата окончания);</span><span class="sxs-lookup"><span data-stu-id="0f67f-194">Planned End Date</span></span>
- <span data-ttu-id="0f67f-195">Work Start Date (Дата начала работы);</span><span class="sxs-lookup"><span data-stu-id="0f67f-195">Work Start Date</span></span>
- <span data-ttu-id="0f67f-196">Work End Date (Дата окончания работы);</span><span class="sxs-lookup"><span data-stu-id="0f67f-196">Work End Date</span></span>
- <span data-ttu-id="0f67f-197">Описание</span><span class="sxs-lookup"><span data-stu-id="0f67f-197">Description</span></span>
- <span data-ttu-id="0f67f-198">Компьютер</span><span class="sxs-lookup"><span data-stu-id="0f67f-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="0f67f-199">Выходные данные инцидента ServiceNow</span><span class="sxs-lookup"><span data-stu-id="0f67f-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="0f67f-200">Поле OMS</span><span class="sxs-lookup"><span data-stu-id="0f67f-200">OMS field</span></span> | <span data-ttu-id="0f67f-201">Поле ITSM</span><span class="sxs-lookup"><span data-stu-id="0f67f-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="0f67f-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-202">ServiceDeskId_s</span></span>| <span data-ttu-id="0f67f-203">Number</span><span class="sxs-lookup"><span data-stu-id="0f67f-203">Number</span></span> |
| <span data-ttu-id="0f67f-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-204">IncidentState_s</span></span> | <span data-ttu-id="0f67f-205">Состояние</span><span class="sxs-lookup"><span data-stu-id="0f67f-205">State</span></span> |
| <span data-ttu-id="0f67f-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-206">Urgency_s</span></span> |<span data-ttu-id="0f67f-207">"Срочность";</span><span class="sxs-lookup"><span data-stu-id="0f67f-207">Urgency</span></span> |
| <span data-ttu-id="0f67f-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-208">Impact_s</span></span> |<span data-ttu-id="0f67f-209">Влияние</span><span class="sxs-lookup"><span data-stu-id="0f67f-209">Impact</span></span>|
| <span data-ttu-id="0f67f-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-210">Priority_s</span></span> | <span data-ttu-id="0f67f-211">Приоритет</span><span class="sxs-lookup"><span data-stu-id="0f67f-211">Priority</span></span> |
| <span data-ttu-id="0f67f-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-212">CreatedBy_s</span></span> | <span data-ttu-id="0f67f-213">Opened by (Кем открыто)</span><span class="sxs-lookup"><span data-stu-id="0f67f-213">Opened by</span></span> |
| <span data-ttu-id="0f67f-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-214">ResolvedBy_s</span></span> | <span data-ttu-id="0f67f-215">"Кем разрешено"</span><span class="sxs-lookup"><span data-stu-id="0f67f-215">Resolved by</span></span>|
| <span data-ttu-id="0f67f-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-216">ClosedBy_s</span></span>  | <span data-ttu-id="0f67f-217">Closed By (Кем закрыто)</span><span class="sxs-lookup"><span data-stu-id="0f67f-217">Closed by</span></span> |
| <span data-ttu-id="0f67f-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-218">Source_s</span></span>| <span data-ttu-id="0f67f-219">Contact type (Тип контакта)</span><span class="sxs-lookup"><span data-stu-id="0f67f-219">Contact type</span></span> |
| <span data-ttu-id="0f67f-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-220">AssignedTo_s</span></span> | <span data-ttu-id="0f67f-221">Кому назначено</span><span class="sxs-lookup"><span data-stu-id="0f67f-221">Assigned to</span></span>  |
| <span data-ttu-id="0f67f-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-222">Category_s</span></span> | <span data-ttu-id="0f67f-223">Категория</span><span class="sxs-lookup"><span data-stu-id="0f67f-223">Category</span></span> |
| <span data-ttu-id="0f67f-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-224">Title_s</span></span>|  <span data-ttu-id="0f67f-225">Краткое описание</span><span class="sxs-lookup"><span data-stu-id="0f67f-225">Short description</span></span> |
| <span data-ttu-id="0f67f-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-226">Description_s</span></span>|  <span data-ttu-id="0f67f-227">Примечания</span><span class="sxs-lookup"><span data-stu-id="0f67f-227">Notes</span></span> |
| <span data-ttu-id="0f67f-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="0f67f-228">CreatedDate_t</span></span>|  <span data-ttu-id="0f67f-229">Opened (Открыто)</span><span class="sxs-lookup"><span data-stu-id="0f67f-229">Opened</span></span> |
| <span data-ttu-id="0f67f-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="0f67f-230">ClosedDate_t</span></span>| <span data-ttu-id="0f67f-231">closed</span><span class="sxs-lookup"><span data-stu-id="0f67f-231">closed</span></span>|
| <span data-ttu-id="0f67f-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="0f67f-232">ResolvedDate_t</span></span>|<span data-ttu-id="0f67f-233">"Разрешено"</span><span class="sxs-lookup"><span data-stu-id="0f67f-233">Resolved</span></span>|
| <span data-ttu-id="0f67f-234">Компьютер</span><span class="sxs-lookup"><span data-stu-id="0f67f-234">Computer</span></span>  | <span data-ttu-id="0f67f-235">Элемент конфигурации</span><span class="sxs-lookup"><span data-stu-id="0f67f-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="0f67f-236">Выходные данные запроса на изменение ServiceNow</span><span class="sxs-lookup"><span data-stu-id="0f67f-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="0f67f-237">Поле OMS</span><span class="sxs-lookup"><span data-stu-id="0f67f-237">OMS field</span></span> | <span data-ttu-id="0f67f-238">Поле ITSM</span><span class="sxs-lookup"><span data-stu-id="0f67f-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="0f67f-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-239">ServiceDeskId_s</span></span>| <span data-ttu-id="0f67f-240">Number</span><span class="sxs-lookup"><span data-stu-id="0f67f-240">Number</span></span> |
| <span data-ttu-id="0f67f-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-241">CreatedBy_s</span></span> | <span data-ttu-id="0f67f-242">"Кем запрошено"</span><span class="sxs-lookup"><span data-stu-id="0f67f-242">Requested by</span></span> |
| <span data-ttu-id="0f67f-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-243">ClosedBy_s</span></span> | <span data-ttu-id="0f67f-244">Closed By (Кем закрыто)</span><span class="sxs-lookup"><span data-stu-id="0f67f-244">Closed by</span></span> |
| <span data-ttu-id="0f67f-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-245">AssignedTo_s</span></span> | <span data-ttu-id="0f67f-246">Кому назначено</span><span class="sxs-lookup"><span data-stu-id="0f67f-246">Assigned to</span></span>  |
| <span data-ttu-id="0f67f-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-247">Title_s</span></span>|  <span data-ttu-id="0f67f-248">Краткое описание</span><span class="sxs-lookup"><span data-stu-id="0f67f-248">Short description</span></span> |
| <span data-ttu-id="0f67f-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-249">Type_s</span></span>|  <span data-ttu-id="0f67f-250">Тип</span><span class="sxs-lookup"><span data-stu-id="0f67f-250">Type</span></span> |
| <span data-ttu-id="0f67f-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-251">Category_s</span></span>|  <span data-ttu-id="0f67f-252">Catgory</span><span class="sxs-lookup"><span data-stu-id="0f67f-252">Catgory</span></span> |
| <span data-ttu-id="0f67f-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-253">CRState_s</span></span>|  <span data-ttu-id="0f67f-254">Состояние</span><span class="sxs-lookup"><span data-stu-id="0f67f-254">State</span></span>|
| <span data-ttu-id="0f67f-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-255">Urgency_s</span></span>|  <span data-ttu-id="0f67f-256">"Срочность";</span><span class="sxs-lookup"><span data-stu-id="0f67f-256">Urgency</span></span> |
| <span data-ttu-id="0f67f-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-257">Priority_s</span></span>| <span data-ttu-id="0f67f-258">Приоритет</span><span class="sxs-lookup"><span data-stu-id="0f67f-258">Priority</span></span>|
| <span data-ttu-id="0f67f-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-259">Risk_s</span></span>| <span data-ttu-id="0f67f-260">"Риск";</span><span class="sxs-lookup"><span data-stu-id="0f67f-260">Risk</span></span>|
| <span data-ttu-id="0f67f-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-261">Impact_s</span></span>| <span data-ttu-id="0f67f-262">Влияние</span><span class="sxs-lookup"><span data-stu-id="0f67f-262">Impact</span></span>|
| <span data-ttu-id="0f67f-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="0f67f-263">RequestedDate_t</span></span>  | <span data-ttu-id="0f67f-264">Requested by date</span><span class="sxs-lookup"><span data-stu-id="0f67f-264">Requested by date</span></span> |
| <span data-ttu-id="0f67f-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="0f67f-265">ClosedDate_t</span></span> | <span data-ttu-id="0f67f-266">Closed Date (Дата закрытия)</span><span class="sxs-lookup"><span data-stu-id="0f67f-266">Closed date</span></span> |
| <span data-ttu-id="0f67f-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="0f67f-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="0f67f-268">Planned Start Date (Планируемая дата начала)</span><span class="sxs-lookup"><span data-stu-id="0f67f-268">Planned start date</span></span> |
| <span data-ttu-id="0f67f-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="0f67f-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="0f67f-270">Planned End Date (Планируемая дата окончания)</span><span class="sxs-lookup"><span data-stu-id="0f67f-270">Planned end date</span></span> |
| <span data-ttu-id="0f67f-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="0f67f-271">WorkStartDate_t</span></span>  | <span data-ttu-id="0f67f-272">Actual start date (Фактическая дата начала)</span><span class="sxs-lookup"><span data-stu-id="0f67f-272">Actual start date</span></span> |
| <span data-ttu-id="0f67f-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="0f67f-273">WorkEndDate_t</span></span> | <span data-ttu-id="0f67f-274">Actual end date (Фактическая дата окончания)</span><span class="sxs-lookup"><span data-stu-id="0f67f-274">Actual end date</span></span>|
| <span data-ttu-id="0f67f-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="0f67f-275">Description_s</span></span> | <span data-ttu-id="0f67f-276">Описание</span><span class="sxs-lookup"><span data-stu-id="0f67f-276">Description</span></span> |
| <span data-ttu-id="0f67f-277">Компьютер</span><span class="sxs-lookup"><span data-stu-id="0f67f-277">Computer</span></span>  | <span data-ttu-id="0f67f-278">Элемент конфигурации</span><span class="sxs-lookup"><span data-stu-id="0f67f-278">Configuration Item</span></span> |

<span data-ttu-id="0f67f-279">**Снимок экрана с примером Log Analytics для данных ITSM:**</span><span class="sxs-lookup"><span data-stu-id="0f67f-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Снимок экрана с Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="0f67f-281">Интеграция соединителя управления ИТ-службами с другими решениями OMS</span><span class="sxs-lookup"><span data-stu-id="0f67f-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="0f67f-282">Сейчас соединитель управления ИТ-службами поддерживает интеграцию с решением схемы услуги.</span><span class="sxs-lookup"><span data-stu-id="0f67f-282">IT Service Management Connector, currently supports integration with the Service Map solution.</span></span>

<span data-ttu-id="0f67f-283">Служба схемы услуги автоматически обнаруживает компоненты приложений в системах Windows и Linux и сопоставляет взаимодействие между службами.</span><span class="sxs-lookup"><span data-stu-id="0f67f-283">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="0f67f-284">Это решение позволяет рассматривать серверы как взаимосвязанные системы, предоставляющие важные службы.</span><span class="sxs-lookup"><span data-stu-id="0f67f-284">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="0f67f-285">Схема услуги отображает сведения о подключениях между серверами, процессами и портами в любой подключенной по протоколу TCP архитектуре без дополнительной настройки. Пользователям требуется только установить агент.</span><span class="sxs-lookup"><span data-stu-id="0f67f-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="0f67f-286">Дополнительные сведения см. в статье [Использование решения схемы услуги в Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="0f67f-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="0f67f-287">Благодаря этой интеграции вы можете просматривать элементы службы поддержки, созданные в решениях ITSM, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="0f67f-287">With this integration, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![<span data-ttu-id="0f67f-288">Интегрированное решение</span><span class="sxs-lookup"><span data-stu-id="0f67f-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="0f67f-289">Создание рабочих элементов ITSM для оповещений OMS</span><span class="sxs-lookup"><span data-stu-id="0f67f-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="0f67f-290">Для оповещений OMS можно создать связанные рабочие элементы в подключенных источниках ITSM.</span><span class="sxs-lookup"><span data-stu-id="0f67f-290">For the OMS alerts, you can create associated work items in the connected ITSM sources.</span></span>  <span data-ttu-id="0f67f-291">Для этого сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="0f67f-291">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="0f67f-292">Запустите запрос поиска по журналам в окне **Поиск по журналу**, чтобы просмотреть данные.</span><span class="sxs-lookup"><span data-stu-id="0f67f-292">From **Log Search** window, run a log search query to view data.</span></span> <span data-ttu-id="0f67f-293">Результаты запроса служат источником для рабочих элементов.</span><span class="sxs-lookup"><span data-stu-id="0f67f-293">Query results are the source for work items.</span></span>
2. <span data-ttu-id="0f67f-294">В разделе **Поиск по журналу** щелкните **Оповещение**, чтобы открыть страницу **Добавить правило оповещения**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-294">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span></span>

    ![Снимок экрана с Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="0f67f-296">В окне **Добавить правило оповещения** предоставьте необходимые сведения в полях **Имя**, **Серьезность**, **Поисковый запрос**, а также укажите **критерии оповещения** (временное окно и единицы измерения).</span><span class="sxs-lookup"><span data-stu-id="0f67f-296">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="0f67f-297">Для **Действия: ITSM** выберите значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="0f67f-298">Выберите подключение ITSM из списка **Выбрать подключение**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-298">Select your ITSM connection from the **Select Connection** list.</span></span>
6. <span data-ttu-id="0f67f-299">Предоставьте необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="0f67f-299">Provide the details as required.</span></span>
7. <span data-ttu-id="0f67f-300">Чтобы создать отдельный рабочий элемент для каждой записи журнала для этого оповещения, установите флажок **Создать отдельные рабочие элементы для каждой записи журнала**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-300">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="0f67f-301">Или</span><span class="sxs-lookup"><span data-stu-id="0f67f-301">Or</span></span>

    <span data-ttu-id="0f67f-302">Не устанавливайте этот флажок, если вы хотите создать только один рабочий элемент для любого количества записей журнала для этого оповещения.</span><span class="sxs-lookup"><span data-stu-id="0f67f-302">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="0f67f-303">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-303">Click **Save**.</span></span>

<span data-ttu-id="0f67f-304">Оповещение OMS будет создано в разделе **Оповещения**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-304">The OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="0f67f-305">Соответствующие рабочие элементы подключения ITSM создаются, когда выполняются указанные условия оповещений.</span><span class="sxs-lookup"><span data-stu-id="0f67f-305">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="0f67f-306">Создание рабочих элементов ITSM из журналов OMS</span><span class="sxs-lookup"><span data-stu-id="0f67f-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="0f67f-307">Вы можете создать рабочие элементы в подключенных источниках ITSM с помощью OMS Log Search.</span><span class="sxs-lookup"><span data-stu-id="0f67f-307">You can create work items in the connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="0f67f-308">Для этого сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="0f67f-308">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="0f67f-309">Выполните поиск необходимых данных в разделе **Поиск по журналу**, выберите данные и щелкните **Create work item** (Создать рабочий элемент).</span><span class="sxs-lookup"><span data-stu-id="0f67f-309">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span></span>

    <span data-ttu-id="0f67f-310">Отобразится окно **Create ITSM Work item** (Создание рабочего элемента ITSM):</span><span class="sxs-lookup"><span data-stu-id="0f67f-310">The **Create ITSM Work item** window appears:</span></span>

    ![Снимок экрана с Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="0f67f-312">Добавьте следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="0f67f-312">Add the following details:</span></span>

  - <span data-ttu-id="0f67f-313">**Название рабочего элемента.** Имя рабочего элемента.</span><span class="sxs-lookup"><span data-stu-id="0f67f-313">**Work item Title**: Title for the work item.</span></span>
  - <span data-ttu-id="0f67f-314">**Описание рабочего элемента.** Описание нового рабочего элемента.</span><span class="sxs-lookup"><span data-stu-id="0f67f-314">**Work item Description**: Description for the new work item.</span></span>
  - <span data-ttu-id="0f67f-315">**Задействованный компьютер.** Имя компьютера, на котором находятся данные журналов.</span><span class="sxs-lookup"><span data-stu-id="0f67f-315">**Affected Computer**: Name of the computer where this log data was found.</span></span>
  - <span data-ttu-id="0f67f-316">**Выбрать подключение.** Подключение ITSM, в котором требуется создать рабочий элемент.</span><span class="sxs-lookup"><span data-stu-id="0f67f-316">**Select Connection**:  ITSM connection in which you want to create this work item.</span></span>
  - <span data-ttu-id="0f67f-317">**Рабочий элемент.** Тип рабочего элемента.</span><span class="sxs-lookup"><span data-stu-id="0f67f-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="0f67f-318">Чтобы использовать имеющейся шаблон рабочего элемента для инцидента, установите для параметра **Generate work item based on the template** (Создать рабочий элемент на основе шаблона) значение **Да** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-318">To use an existing work item template for an incident, click **Yes** under **Generate work item based on the template** option and then click **Create**.</span></span>

    <span data-ttu-id="0f67f-319">или</span><span class="sxs-lookup"><span data-stu-id="0f67f-319">Or,</span></span>

    <span data-ttu-id="0f67f-320">Если вы хотите предоставить собственные настраиваемые значения, щелкните **Нет**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-320">Click **No** if you want to provide your customized values.</span></span>

4. <span data-ttu-id="0f67f-321">Предоставьте соответствующие значения в текстовых полях **Тип контакта**, **Воздействие**, **Срочность**, **Категория** и **Подкатегория**, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-321">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="0f67f-322">В ITSM будет создан рабочий элемент, который вы также можете просмотреть в OMS.</span><span class="sxs-lookup"><span data-stu-id="0f67f-322">The work item will be created in the ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="0f67f-323">Устранение неполадок с подключением ITSM в OMS</span><span class="sxs-lookup"><span data-stu-id="0f67f-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="0f67f-324">Если сбой подключения происходит из пользовательского интерфейса подключенного источника и отображается сообщение **Ошибка при сохранении подключения**, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="0f67f-324">If connection fails from connected source's UI and you get the **Error in saving connection** message, do the following:</span></span>
 - <span data-ttu-id="0f67f-325">При использовании подключений ServiceNow, Cherwell и Provance проверьте имя пользователя и пароль, а также идентификатор и секрет клиента каждого подключения.</span><span class="sxs-lookup"><span data-stu-id="0f67f-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  the username/password and  client ID/client secret  for each of the connections.</span></span> <span data-ttu-id="0f67f-326">Если ошибка не исчезнет, проверьте наличие необходимых прав в соответствующем продукте ITSM, чтобы установить подключение.</span><span class="sxs-lookup"><span data-stu-id="0f67f-326">If the error persists, check if you have sufficient privileges  in the corresponding ITSM product to make the connection.</span></span>
 - <span data-ttu-id="0f67f-327">При использовании Service Manager убедитесь, что веб-приложение успешно развернуто и создано гибридное подключение.</span><span class="sxs-lookup"><span data-stu-id="0f67f-327">In case of Service Manager, ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="0f67f-328">Чтобы проверить подключение к локальному компьютеру Service Manager, перейдите по URL-адресу веб-приложения, как описано в документации по установке [гибридного подключения](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="0f67f-328">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="0f67f-329">Если данные из ServiceNow не синхронизируются с OMS, убедитесь, что экземпляр ServiceNow не находится в спящем режиме.</span><span class="sxs-lookup"><span data-stu-id="0f67f-329">If data from ServiceNow is not getting synced in OMS, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="0f67f-330">Иногда эта ошибка может происходить в экземплярах ServiceNow во время простоя.</span><span class="sxs-lookup"><span data-stu-id="0f67f-330">This might sometime happen in the ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="0f67f-331">В противном случае сообщите о проблеме.</span><span class="sxs-lookup"><span data-stu-id="0f67f-331">Else, report the issue.</span></span>
3.  <span data-ttu-id="0f67f-332">Если оповещения поступают из OMS, но рабочие элементы не создаются в продукте ITSM или элементы конфигурации не создаются и (или) связываются с рабочими элементами, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="0f67f-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked to work items or for any generic information, do the following:</span></span>
 -  <span data-ttu-id="0f67f-333">С помощью решения "Соединитель управления ИТ-службами" на портале OMS соберите сводные данные о подключениях, рабочих элементах, компьютерах и т. д. Щелкните сообщение об ошибке в колонке состояния, перейдите на страницу **Поиск по журналам** и просмотрите подключение с ошибкой, используя сведения в сообщении.</span><span class="sxs-lookup"><span data-stu-id="0f67f-333">IT Service Management Connector solution in OMS portal could be used to get a summary of connections/work items/computers etc. Click the error message in the status blade, navigate to **Log Search** and view the connection that has the error by using the details in the error message.</span></span>
 - <span data-ttu-id="0f67f-334">Сведения об ошибках и другие связанные сведения можно просмотреть непосредственно на странице **Поиск по журналам** с помощью *Type=ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="0f67f-334">you can directly view the errors/related information in the **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="0f67f-335">Устранение неполадок развертывания веб-приложения Service Manager</span><span class="sxs-lookup"><span data-stu-id="0f67f-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="0f67f-336">При наличии неполадок с развертыванием веб-приложения проверьте наличие всех необходимых разрешений в подписке, используемой для создания или развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0f67f-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="0f67f-337">Если во время выполнения [скрипта](log-analytics-itsmc-service-manager-script.md) отображается сообщение **Ссылка на объект не указывает на экземпляр объекта**, проверьте значения в разделе **Конфигурация пользователя**.</span><span class="sxs-lookup"><span data-stu-id="0f67f-337">If **Object reference not set to instance of an object** error message appears while running the [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="0f67f-338">Если вам не удается создать пространство имен ретранслятора шины обслуживания, убедитесь, в подписке зарегистрирован требуемый поставщик ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0f67f-338">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="0f67f-339">Если не зарегистрирован, создайте его на портале Azure вручную.</span><span class="sxs-lookup"><span data-stu-id="0f67f-339">If not registered, manually create it from the Azure portal.</span></span> <span data-ttu-id="0f67f-340">Его также можно создать на портале Azure во время создания [гибридного подключения](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="0f67f-340">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="0f67f-341">Свяжитесь с нами</span><span class="sxs-lookup"><span data-stu-id="0f67f-341">Contact us</span></span>

<span data-ttu-id="0f67f-342">Свяжитесь с нами по адресу [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com), чтобы оставить отзывы или запросы касательно соединителя управления ИТ-службами.</span><span class="sxs-lookup"><span data-stu-id="0f67f-342">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f67f-343">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f67f-343">Next steps</span></span>
<span data-ttu-id="0f67f-344">[Подключение продуктов и служб ITSM с помощью соединителя управления ИТ-службами (предварительная версия)](log-analytics-itsmc-connections.md)</span><span class="sxs-lookup"><span data-stu-id="0f67f-344">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
