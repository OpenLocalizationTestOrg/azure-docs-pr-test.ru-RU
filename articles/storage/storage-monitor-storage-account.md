---
title: "Как отслеживать учетную запись хранения Azure | Документация Майкрософт"
description: "Выполнение мониторинга учетной записи хранения в Azure с помощью портала Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: b49e06da0019a50cc8e50c4da47e42c03b44bcc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-storage-account-in-the-azure-portal"></a><span data-ttu-id="2c63f-103">Мониторинг учетной записи хранения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="2c63f-103">Monitor a storage account in the Azure portal</span></span>

<span data-ttu-id="2c63f-104">[Аналитика службы хранилища Azure](storage-analytics.md) предоставляет метрики для всех служб хранилища и журналы для больших двоичных объектов, очередей и таблиц.</span><span class="sxs-lookup"><span data-stu-id="2c63f-104">[Azure Storage Analytics](storage-analytics.md) provides metrics for all storage services, and logs for blobs, queues, and tables.</span></span> <span data-ttu-id="2c63f-105">С помощью [портала Azure](https://portal.azure.com) можно настроить метрики и журналы, записываемые для вашей учетной записи, а также настроить диаграммы, которые обеспечивают визуальное представление данных этих метрик.</span><span class="sxs-lookup"><span data-stu-id="2c63f-105">You can use the [Azure portal](https://portal.azure.com) to configure which metrics and logs are recorded for your account, and configure charts that provide visual representations of your metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="2c63f-106">За изучение данных мониторинга на портале Azure взимается плата.</span><span class="sxs-lookup"><span data-stu-id="2c63f-106">There are costs associated with examining monitoring data in the Azure portal.</span></span> <span data-ttu-id="2c63f-107">Дополнительные сведения см. в разделе [Аналитика и выставление счетов для хранилища](/rest/api/storageservices/Storage-Analytics-and-Billing).</span><span class="sxs-lookup"><span data-stu-id="2c63f-107">For more information, see [Storage Analytics and Billing](/rest/api/storageservices/Storage-Analytics-and-Billing).</span></span>
>
> <span data-ttu-id="2c63f-108">В настоящий момент файловое хранилище Azure поддерживает метрики Storage Analytics, но не поддерживает ведение журналов.</span><span class="sxs-lookup"><span data-stu-id="2c63f-108">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>
> <span data-ttu-id="2c63f-109">В настоящее время учетные записи хранения, использующие репликацию типа ZRS (хранилище, избыточное в пределах зоны), не имеют действующих функций метрик или ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="2c63f-109">Storage accounts with a replication type of Zone-Redundant Storage (ZRS) currently do not have the metrics or logging capability enabled.</span></span>
> 
> <span data-ttu-id="2c63f-110">Дополнительные указания о функциях аналитики хранилища и других инструментах идентификации, диагностики и устранения неполадок, связанных со службой хранилища Azure, см. в статье [Мониторинг, диагностика и устранение неполадок службы хранилища Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2c63f-110">For an in-depth guide on using Storage Analytics and other tools to identify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>
>

## <a name="configure-monitoring-for-a-storage-account"></a><span data-ttu-id="2c63f-111">Настройка мониторинга учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="2c63f-111">Configure monitoring for a storage account</span></span>

1. <span data-ttu-id="2c63f-112">На [портале Azure](https://portal.azure.com) выберите **Учетные записи хранения**, а затем щелкните имя учетной записи хранения, чтобы открыть ее панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="2c63f-112">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the storage account name to open the account dashboard.</span></span>
1. <span data-ttu-id="2c63f-113">В колонке меню в разделе **Мониторинг** щелкните **Диагностика**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-113">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![Параметры мониторинга](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. <span data-ttu-id="2c63f-115">Выберите **тип** данных метрик для каждой **службы**, которую нужно отслеживать, и **политику хранения** для данных.</span><span class="sxs-lookup"><span data-stu-id="2c63f-115">Select the **type** of metrics data for each **service** you wish to monitor, and the **retention policy** for the data.</span></span> <span data-ttu-id="2c63f-116">Можно также отключить мониторинг, задав для параметра **Состояние** значение **Откл**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-116">You can also disable monitoring by setting **Status** to **Off**.</span></span>

    ![Параметры мониторинга](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   <span data-ttu-id="2c63f-118">Существуют два типа метрик, которые можно включить для каждой службы. Они включены по умолчанию для новых учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="2c63f-118">There are two types of metrics you can enable for each service, both of which are enabled by default for new storage accounts:</span></span>

   * <span data-ttu-id="2c63f-119">**Сводная**: позволяет собирать такие метрики, как метрики исходящего и входящего трафика, доступности, задержки и процента успешных операций.</span><span class="sxs-lookup"><span data-stu-id="2c63f-119">**Aggregate**: Collects metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="2c63f-120">Эти метрики вычисляются для служб BLOB-объектов, очередей, таблиц и файлов.</span><span class="sxs-lookup"><span data-stu-id="2c63f-120">These metrics are aggregated for the blob, queue, table, and file services.</span></span>
   * <span data-ttu-id="2c63f-121">**Для каждого API**: в дополнение к сводным метрикам позволяет собирать одинаковый набор метрик для каждой операции с хранилищем в API службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="2c63f-121">**Per API**: In addition to the aggregate metrics, collects the same set of metrics for each storage operation in the Azure Storage service API.</span></span>

   <span data-ttu-id="2c63f-122">Чтобы задать политику хранения данных, переместите ползунок **Хранение (дни)** или введите число дней хранения данных в диапазоне от 1 до 365.</span><span class="sxs-lookup"><span data-stu-id="2c63f-122">To set the data retention policy, move the **Retention (days)** slider or enter the number of days of data to retain, from 1 to 365.</span></span> <span data-ttu-id="2c63f-123">Значение по умолчанию для новых учетных записей хранения составляет семь дней.</span><span class="sxs-lookup"><span data-stu-id="2c63f-123">The default for new storage accounts is seven days.</span></span> <span data-ttu-id="2c63f-124">Если политику хранения задавать не нужно, введите ноль.</span><span class="sxs-lookup"><span data-stu-id="2c63f-124">If you do not want to set a retention policy, enter zero.</span></span> <span data-ttu-id="2c63f-125">Если политика хранения отсутствует, удаление данных мониторинга выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="2c63f-125">If there is no retention policy, it is up to you to delete the monitoring data.</span></span>

   > [!WARNING]
   > <span data-ttu-id="2c63f-126">За удаление данных метрик вручную взимается плата.</span><span class="sxs-lookup"><span data-stu-id="2c63f-126">You are charged when you manually delete metrics data.</span></span> <span data-ttu-id="2c63f-127">Устаревшие данные аналитики (срок которых превышает значение, установленное политикой хранения) удаляются системой бесплатно.</span><span class="sxs-lookup"><span data-stu-id="2c63f-127">Stale analytics data (data older than your retention policy) is deleted by the system at no cost.</span></span> <span data-ttu-id="2c63f-128">Рекомендуется устанавливать политику хранения в зависимости от того, как долго нужно хранить данные аналитики хранилища для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2c63f-128">We recommend setting a retention policy based on how long you want to retain storage analytics data for your account.</span></span> <span data-ttu-id="2c63f-129">Дополнительные сведения см. в разделе [Какова стоимость включения метрик хранилища?](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics)</span><span class="sxs-lookup"><span data-stu-id="2c63f-129">See [What charges do you incur when you enable storage metrics?](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) for more information.</span></span>
   >

1. <span data-ttu-id="2c63f-130">Закончив настройку мониторинга, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-130">When you finish the monitoring configuration, select **Save**.</span></span>

<span data-ttu-id="2c63f-131">На диаграммах в колонке учетной записи хранения отображается набор метрик по умолчанию, как и в отдельных колонках служб (BLOB-объектов, очередей, таблиц и файлов).</span><span class="sxs-lookup"><span data-stu-id="2c63f-131">A default set of metrics is displayed in charts on the storage account blade, as well as the individual service blades (blob, queue, table, and file).</span></span> <span data-ttu-id="2c63f-132">После включения метрик для службы может пройти до часа, прежде чем их данные отобразятся на диаграммах.</span><span class="sxs-lookup"><span data-stu-id="2c63f-132">Once you've enabled metrics for a service, it may take up to an hour for data to appear in its charts.</span></span> <span data-ttu-id="2c63f-133">Можно щелкнуть **Изменить** на любой диаграмме метрики, чтобы [настроить метрики](#how-to-customize-metrics-charts), отображаемые на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="2c63f-133">You can select **Edit** on any metric chart to [configure which metrics](#how-to-customize-metrics-charts) are displayed in the chart.</span></span>

<span data-ttu-id="2c63f-134">Можно отключить сбор метрик и ведение журнала, задав для параметра **Состояние** значение **Откл**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-134">You can disable metrics collection and logging by setting **Status** to **Off**.</span></span>

> [!NOTE]
> <span data-ttu-id="2c63f-135">Служба хранилища Azure использует [хранилище таблиц](storage-introduction.md#table-storage) для хранения метрик вашей учетной записи хранения и хранит метрики в таблицах, расположенных в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2c63f-135">Azure Storage uses [table storage](storage-introduction.md#table-storage) to store the metrics for your storage account, and stores the metrics in tables in your account.</span></span> <span data-ttu-id="2c63f-136">Дополнительные сведения можно найти в разделе</span><span class="sxs-lookup"><span data-stu-id="2c63f-136">For more information, see.</span></span> <span data-ttu-id="2c63f-137">[Как хранятся метрики](storage-analytics.md#how-metrics-are-stored).</span><span class="sxs-lookup"><span data-stu-id="2c63f-137">[How metrics are stored](storage-analytics.md#how-metrics-are-stored).</span></span>
>

## <a name="customize-metrics-charts"></a><span data-ttu-id="2c63f-138">Настройка диаграмм метрик</span><span class="sxs-lookup"><span data-stu-id="2c63f-138">Customize metrics charts</span></span>

<span data-ttu-id="2c63f-139">Чтобы выбрать метрики хранилища для отображения на диаграмме метрик, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2c63f-139">Use the following procedure to choose which storage metrics to view in a metrics chart.</span></span> 

1. <span data-ttu-id="2c63f-140">Сначала отобразите диаграмму метрики службы хранилища на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2c63f-140">Start by displaying a storage metric chart in the Azure portal.</span></span> <span data-ttu-id="2c63f-141">Диаграммы можно найти в **колонке учетной записи хранения** и в колонке **Метрики** для отдельных служб (BLOB-объектов, очередей, таблиц, файлов).</span><span class="sxs-lookup"><span data-stu-id="2c63f-141">You can find charts on the **storage account blade** and in the **Metrics** blade for an individual service (blob, queue, table, file).</span></span>

   <span data-ttu-id="2c63f-142">В этом примере мы используем приведенную ниже диаграмму, которая отображается в **колонке учетной записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-142">In this example, we work with the following chart that appears on the **storage account blade**:</span></span>

   ![Выбор диаграммы на портале Azure](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. <span data-ttu-id="2c63f-144">Щелкните в любом месте диаграммы, чтобы открыть колонку **Метрика**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-144">Next, click anywhere within the chart to open the **Metric** blade.</span></span> <span data-ttu-id="2c63f-145">Выберите **Изменить диаграмму**, чтобы открыть колонку **Правка диаграммы**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-145">Select **Edit chart** to open the **Edit Chart** blade.</span></span>

   ![Кнопка "Изменить диаграмму" в колонке диаграммы](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. <span data-ttu-id="2c63f-147">В колонке **Правка диаграммы** выберите **Диапазон времени** метрик для отображения на диаграмме и **службу** (BLOB-объектов, очередей, таблиц, файлов), метрики которой нужно отобразить.</span><span class="sxs-lookup"><span data-stu-id="2c63f-147">On the **Edit Chart** blade, select the **Time Range** of the metrics to display in the chart, and the **service** (blob, queue, table, file) whose metrics you wish to display.</span></span> <span data-ttu-id="2c63f-148">Ниже мы выбрали отображение метрик службы BLOB-объектов за прошлую неделю.</span><span class="sxs-lookup"><span data-stu-id="2c63f-148">Here we've selected to display the past week's metrics for the blob service:</span></span>

   ![Выбор диапазона времени и службы в колонке "Правка диаграммы"](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. <span data-ttu-id="2c63f-150">Выберите отдельные **метрики**, которые нужно отобразить на диаграмме, затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-150">Select the individual **metrics** you'd like displayed in the chart, then click **OK**.</span></span> <span data-ttu-id="2c63f-151">Например, здесь мы решили отобразить метрики *ContainerCount* и *ObjectCount*.</span><span class="sxs-lookup"><span data-stu-id="2c63f-151">For example, here we've chosen to display the *ContainerCount* and *ObjectCount* metrics:</span></span>

   ![Выбор отдельных метрик в колонке "Правка диаграммы"](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

<span data-ttu-id="2c63f-153">Параметры диаграммы не влияют на сбор, статистическую обработку или хранение данных мониторинга в учетной записи хранения. Они определяют только отображение данных метрик.</span><span class="sxs-lookup"><span data-stu-id="2c63f-153">Your chart settings do not affect the collection, aggregation, or storage of monitoring data in the storage account, only the viewing of metrics data.</span></span>

### <a name="metrics-availability-in-charts"></a><span data-ttu-id="2c63f-154">Доступность метрики на диаграммах</span><span class="sxs-lookup"><span data-stu-id="2c63f-154">Metrics availability in charts</span></span>

<span data-ttu-id="2c63f-155">Список доступных метрик меняется в зависимости от того, какая служба выбрана из раскрывающегося списка и какой тип единиц использует изменяемая диаграмма.</span><span class="sxs-lookup"><span data-stu-id="2c63f-155">The list of available metrics changes based on which service you've chosen in the drop-down, and the unit type of the chart you're editing.</span></span> <span data-ttu-id="2c63f-156">Например, процентные метрики, такие как *PercentNetworkError* и *PercentThrottlingError*, можно выбрать только в том случае, если требуется изменить диаграмму, показывающую единицы в процентах.</span><span class="sxs-lookup"><span data-stu-id="2c63f-156">For example, you can select percentage metrics like *PercentNetworkError* and *PercentThrottlingError* only if you're editing a chart that displays units in percentage:</span></span>

![Ошибка запроса к процентной диаграмме на портале Azure](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a><span data-ttu-id="2c63f-158">Разрешение метрик</span><span class="sxs-lookup"><span data-stu-id="2c63f-158">Metrics resolution</span></span>

<span data-ttu-id="2c63f-159">Метрики, выбранные в колонке "Диагностика", определяют разрешение метрик, доступных для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2c63f-159">The metrics you selected in Diagnostics determines the resolution of the metrics that are available for your account:</span></span>

* <span data-ttu-id="2c63f-160">**Сводный** мониторинг позволяет собирать такие метрики, как метрики исходящего и входящего трафика, доступности, задержки и процента успешных операций.</span><span class="sxs-lookup"><span data-stu-id="2c63f-160">**Aggregate** monitoring provides metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="2c63f-161">Эти метрики вычисляются для служб BLOB-объектов, очередей, таблиц и файлов.</span><span class="sxs-lookup"><span data-stu-id="2c63f-161">These metrics are aggregated from the blob, table, file, and queue services.</span></span>
* <span data-ttu-id="2c63f-162">Мониторинг **каждого API** обеспечивает более точное разрешение, помимо статистических метрик уровня службы предоставляя метрики отдельных операций хранилища.</span><span class="sxs-lookup"><span data-stu-id="2c63f-162">**Per API** provides finer resolution, with metrics available for individual storage operations, in addition to the service-level aggregates.</span></span>

## <a name="configure-metrics-alerts"></a><span data-ttu-id="2c63f-163">Настройка оповещений метрик</span><span class="sxs-lookup"><span data-stu-id="2c63f-163">Configure metrics alerts</span></span>

<span data-ttu-id="2c63f-164">Можно создать оповещения, чтобы получать уведомления о достижении пороговых значений для метрик ресурсов хранилища.</span><span class="sxs-lookup"><span data-stu-id="2c63f-164">You can create alerts to notify you when thresholds have been reached for storage resource metrics.</span></span>

1. <span data-ttu-id="2c63f-165">Чтобы открыть **колонку правил генерации оповещений**, прокрутите **колонку меню** вниз до раздела **Мониторинг** и выберите **Правила генерации оповещений**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-165">To open the **Alert rules blade**, scroll down to the **MONITORING** section of the **Menu blade** and select **Alert rules**.</span></span>
1. <span data-ttu-id="2c63f-166">Выберите **Добавить оповещение**, чтобы открыть колонку **Добавление правила оповещения**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-166">Select **Add alert** to open the **Add an alert rule** blade</span></span>
1. <span data-ttu-id="2c63f-167">Выберите **ресурс** (большой двоичный объект, файл, очередь, таблицу) из раскрывающегося списка и введите **имя** и **описание** нового правила генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="2c63f-167">Select a **Resource** (blob, file, queue, table) from the drop-down, and enter a **Name** and **Description** for your new alert rule.</span></span>
1. <span data-ttu-id="2c63f-168">Выберите **метрику**, для которой нужно добавить оповещение, и укажите **условие** и **пороговое значение** оповещения.</span><span class="sxs-lookup"><span data-stu-id="2c63f-168">Select the **Metric** for which you'd like to add an alert, an alert **Condition**, and a **Threshold**.</span></span> <span data-ttu-id="2c63f-169">Тип единицы порогового значения меняется в зависимости от выбранной метрики.</span><span class="sxs-lookup"><span data-stu-id="2c63f-169">The threshold unit type changes depending on the metric you've chosen.</span></span> <span data-ttu-id="2c63f-170">Например, "количество" — тип единицы измерения для *ContainerCount*, тогда как единицей измерения для метрики *PercentNetworkError* является процент.</span><span class="sxs-lookup"><span data-stu-id="2c63f-170">For example, "count" is the unit type for *ContainerCount*, while the unit for the *PercentNetworkError* metric is a percentage.</span></span>
1. <span data-ttu-id="2c63f-171">Выберите **период**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-171">Select the **Period**.</span></span> <span data-ttu-id="2c63f-172">Если метрика достигает порогового значения или превышает его в течение периода, активируется оповещение.</span><span class="sxs-lookup"><span data-stu-id="2c63f-172">Metrics that reach or exceed the Threshold within the period trigger an alert.</span></span>
1. <span data-ttu-id="2c63f-173">(Необязательно.) Настройте уведомления с использованием **электронного адреса** и **webhook**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-173">(Optional) Configure **Email** and **Webhook** notifications.</span></span> <span data-ttu-id="2c63f-174">Дополнительные сведения об объектах webhook см. в разделе [Настройка объектов webhook для оповещений на основе метрик Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="2c63f-174">For more information on webhooks, see [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="2c63f-175">Если не настроить уведомления с помощью электронной почты или webhook, то они будут отображаться только на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2c63f-175">If you do not configure email or webhook notifications, alerts will appear only in the Azure portal.</span></span>

![Колонка "Добавление правила оповещения" на портале Azure](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-to-the-portal-dashboard"></a><span data-ttu-id="2c63f-177">Добавление диаграмм метрик на панель мониторинга портала</span><span class="sxs-lookup"><span data-stu-id="2c63f-177">Add metrics charts to the portal dashboard</span></span>

<span data-ttu-id="2c63f-178">Диаграммы метрик службы хранилища Azure для любых учетных записей хранения можно добавить на панель мониторинга портала.</span><span class="sxs-lookup"><span data-stu-id="2c63f-178">You can add Azure Storage metrics charts for any of your storage accounts to your portal dashboard.</span></span>

1. <span data-ttu-id="2c63f-179">Откройте панель мониторинга на [портале Azure](https://portal.azure.com) и щелкните **Изменить панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-179">Select click **Edit dashboard** while viewing your dashboard in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="2c63f-180">В колонке **Коллекция плиток** выберите **Найти плитки по** > **Тип**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-180">In the **Tile Gallery**, select **Find tiles by** > **Type**.</span></span>
1. <span data-ttu-id="2c63f-181">Выберите **Тип** > **Учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-181">Select **Type** > **Storage accounts**.</span></span>
1. <span data-ttu-id="2c63f-182">В колонке **ресурсы** выберите учетную запись, метрики которой вы хотите добавить на панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="2c63f-182">In **Resources**, select the storage account whose metrics you wish to add to the dashboard.</span></span>
1. <span data-ttu-id="2c63f-183">Выберите **Категории** > **Мониторинг**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-183">Select **Categories** > **Monitoring**.</span></span>
1. <span data-ttu-id="2c63f-184">Перетащите на панель мониторинга элемент диаграммы для метрики, которую нужно отобразить.</span><span class="sxs-lookup"><span data-stu-id="2c63f-184">Drag-and-drop the chart tile onto your dashboard for the metric you'd like displayed.</span></span> <span data-ttu-id="2c63f-185">Повторите это для всех метрик, которые требуется отобразить на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="2c63f-185">Repeat for all metrics you'd like displayed on the dashboard.</span></span> <span data-ttu-id="2c63f-186">На следующем рисунке в качестве примера выбрана диаграмма "Большие двоичные объекты — всего запросов", но на панель мониторинга можно добавить любую диаграмму.</span><span class="sxs-lookup"><span data-stu-id="2c63f-186">In the following image, the "Blobs - Total requests" chart is highlighted as an example, but all the charts are available for placement on your dashboard.</span></span>

   ![Коллекция элементов на портале Azure](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. <span data-ttu-id="2c63f-188">Завершив добавление диаграммы, выберите **Настройка выполнена** в верхней части панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="2c63f-188">Select **Done customizing** near the top of the dashboard when you're done adding charts.</span></span>

<span data-ttu-id="2c63f-189">После добавления диаграмм на панель мониторинга их можно настроить, как описано в разделе [Настройка диаграмм метрик](#how-to-customize-metrics-charts).</span><span class="sxs-lookup"><span data-stu-id="2c63f-189">Once you've added charts to your dashboard, you can further customize them as described in [Customize metrics charts](#how-to-customize-metrics-charts).</span></span>

## <a name="configure-logging"></a><span data-ttu-id="2c63f-190">Настройка журнала</span><span class="sxs-lookup"><span data-stu-id="2c63f-190">Configure logging</span></span>

<span data-ttu-id="2c63f-191">Можно указать службе хранилища Azure сохранять журналы диагностики для запросов на чтение, запись и удаление, отправляемых к службам BLOB-объектов, таблиц и очередей.</span><span class="sxs-lookup"><span data-stu-id="2c63f-191">You can instruct Azure Storage to save diagnostics logs for read, write, and delete requests for the blob, table, and queue services.</span></span> <span data-ttu-id="2c63f-192">Заданная политика хранения данных также применяется к этим журналам.</span><span class="sxs-lookup"><span data-stu-id="2c63f-192">The data retention policy you set also applies to these logs.</span></span>

> [!NOTE]
> <span data-ttu-id="2c63f-193">В настоящий момент файловое хранилище Azure поддерживает метрики Storage Analytics, но не поддерживает ведение журналов.</span><span class="sxs-lookup"><span data-stu-id="2c63f-193">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>

1. <span data-ttu-id="2c63f-194">На [портале Azure](https://portal.azure.com) выберите **Учетные записи хранения**, а затем щелкните имя учетной записи хранения, чтобы открыть ее колонку.</span><span class="sxs-lookup"><span data-stu-id="2c63f-194">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the name of the storage account to open the storage account blade.</span></span>
1. <span data-ttu-id="2c63f-195">В колонке меню в разделе **Мониторинг** щелкните **Диагностика**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-195">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![Пункт меню "Диагностика" в разделе "Мониторинг" на портале Azure](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. <span data-ttu-id="2c63f-197">Убедитесь, что параметр **Состояние** имеет значение **Вкл.**, и выберите **службы**, для которых нужно включить ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="2c63f-197">Ensure **Status** is set to **On**, and select the **services** for which you'd like to enable logging.</span></span>

    ![Настройка ведения журнала на портале Azure](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. <span data-ttu-id="2c63f-199">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2c63f-199">Click **Save**.</span></span>

<span data-ttu-id="2c63f-200">Журналы диагностики сохраняются в контейнере BLOB-объектов с именем $logs в вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2c63f-200">The diagnostics logs are saved in a blob container named $logs in your storage account.</span></span> <span data-ttu-id="2c63f-201">Можно просмотреть данные журнала с помощью обозревателя хранилищ, например [Microsoft Storage Explorer](http://storageexplorer.com), или программно, с помощью клиентской библиотеки службы хранилища или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c63f-201">You can view the log data using a storage explorer like the [Microsoft Storage Explorer](http://storageexplorer.com), or programmatically using the storage client library or PowerShell.</span></span>

<span data-ttu-id="2c63f-202">Дополнительные сведения о доступе к контейнеру $logs см. в разделе [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data) (Включение ведения журнала и доступа к данным журнала хранилища).</span><span class="sxs-lookup"><span data-stu-id="2c63f-202">For information about accessing the $logs container, see [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c63f-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c63f-203">Next steps</span></span>

* <span data-ttu-id="2c63f-204">Дополнительные сведения о [метриках, ведении журнала и выставлении счетов](storage-analytics.md) для аналитики службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="2c63f-204">Find more details about [metrics, logging, and billing](storage-analytics.md) for Storage Analytics.</span></span>
* <span data-ttu-id="2c63f-205">[Включение метрик службы хранилища Azure и просмотр данных метрик](storage-enable-and-view-metrics.md) с помощью PowerShell и программно с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="2c63f-205">[Enable Azure Storage metrics and view metrics data](storage-enable-and-view-metrics.md) by using PowerShell and programmatically with C#.</span></span>
