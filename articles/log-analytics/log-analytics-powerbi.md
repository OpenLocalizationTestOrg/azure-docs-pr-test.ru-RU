---
title: "Экспорт данных Log Analytics в Power BI | Документация Майкрософт"
description: "Power BI — это облачная служба бизнес-аналитики от Майкрософт, предоставляющая расширенную визуализацию данных и отчеты по анализу различных наборов данных.  Log Analytics может непрерывно экспортировать данные из репозитория OMS в Power BI, чтобы вы могли использовать предоставляемые службой визуализации и средства анализа.  В этой статье описывается настройка запросов в службе Log Analytics, которые автоматически экспортируются в Power BI с регулярной периодичностью."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 98befb16d27387e8f65a27771a2a32c264119d74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="export-log-analytics-data-to-power-bi"></a><span data-ttu-id="91983-105">Экспорт данных Log Analytics в Power BI</span><span class="sxs-lookup"><span data-stu-id="91983-105">Export Log Analytics data to Power BI</span></span>

>[!NOTE]
> <span data-ttu-id="91983-106">Если ваша рабочая область переведена на [новый язык запросов Log Analytics](log-analytics-log-search-upgrade.md), этот процесс экспорта данных Log Analytics в Power BI больше не будет работать.</span><span class="sxs-lookup"><span data-stu-id="91983-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then this process for exporting Log Analytics data to Power BI will no longer work.</span></span>  <span data-ttu-id="91983-107">Все существующие расписания, созданные перед обновлением, будут отключены.</span><span class="sxs-lookup"><span data-stu-id="91983-107">Any existing schedules that you created before upgrading will become disabled.</span></span> 
>
> <span data-ttu-id="91983-108">После обновления в Azure Log Analytics работает та же платформа, что и в Application Insights, и вы можете использовать для экспорта запросов Log Analytics в Power BI тот же процесс, что и для [экспорта запросов Application Insights в Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span><span class="sxs-lookup"><span data-stu-id="91983-108">After upgrade, Azure Log Analytics uses the same platform as Application Insights, and you use the same process to export Log Analytics queries to Power BI as [the process to export Application Insights queries to Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>  <span data-ttu-id="91983-109">Чтобы экспортировать запрос, можно воспользоваться консолью Analytics, как описано в этой статье, или нажать кнопку **Power BI** в верхней части экрана на портале поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="91983-109">You can either export the query using the Analytics console as described in that article, or you can select the **Power BI** button at the top of the screen in the Log Search portal.</span></span>



<span data-ttu-id="91983-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) — это облачная служба бизнес-аналитики от Майкрософт, предоставляющая расширенную визуализацию данных и отчеты по анализу различных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="91983-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span></span>  <span data-ttu-id="91983-111">Log Analytics может автоматически экспортировать данные из репозитория OMS в Power BI, чтобы вы могли использовать предоставляемые службой визуализации и средства анализа.</span><span class="sxs-lookup"><span data-stu-id="91983-111">Log Analytics can automatically export data from the OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>

<span data-ttu-id="91983-112">Настраивая Power BI с использованием службы Log Analytics, вы создаете запросы журналов, экспортирующие свои результаты в соответствующие наборы данных в Power BI.</span><span class="sxs-lookup"><span data-stu-id="91983-112">When you configure Power BI with Log Analytics, you create log queries that export their results to corresponding datasets in Power BI.</span></span>  <span data-ttu-id="91983-113">Запросы и экспорт продолжают автоматически выполняться по расписанию, установленному вами для обновления набора данных в соответствии с последними данными, собранными службой Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="91983-113">The query and export continues to automatically run on a schedule that you define to keep the dataset up to date with the latest data collected by Log Analytics.</span></span>

![Из Log Analytics в Power BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a><span data-ttu-id="91983-115">Расписания Power BI</span><span class="sxs-lookup"><span data-stu-id="91983-115">Power BI Schedules</span></span>
<span data-ttu-id="91983-116">*Расписание Power BI* включает поиск по журналам, который экспортирует набор данных из репозитория OMS в соответствующий набор данных в Power BI, а также расписание, определяющее периодичность выполнения этого поиска для актуализации набора данных.</span><span class="sxs-lookup"><span data-stu-id="91983-116">A *Power BI Schedule* includes a log search that exports a set of data from the OMS repository to a corresponding dataset in Power BI and a schedule that defines how often this search is run to keep the dataset current.</span></span>

<span data-ttu-id="91983-117">Поля в наборе данных должны соответствовать свойствам записей, возвращаемых в результате поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="91983-117">The fields in the dataset will match the properties of the records returned by the log search.</span></span>  <span data-ttu-id="91983-118">Если поиск выдает записи разных типов, набор данных включает все свойства каждого из включенных типов записей.</span><span class="sxs-lookup"><span data-stu-id="91983-118">If the search returns records of different types then the dataset will include all of the properties from each of the included record types.</span></span>  

> [!NOTE]
> <span data-ttu-id="91983-119">Запрос поиска по журналу, возвращающий необработанные данные, более предпочтителен, чем консолидация с использованием таких команд, как [Measure](log-analytics-search-reference.md#measure).</span><span class="sxs-lookup"><span data-stu-id="91983-119">It is a best practice to use a log search query that returns raw data as opposed to performing any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span></span>  <span data-ttu-id="91983-120">На основе необработанных данных в Power BI можно выполнять любые операции агрегирования и расчеты.</span><span class="sxs-lookup"><span data-stu-id="91983-120">You can perform any aggregation and calculations in Power BI from the raw data.</span></span>
>
>

## <a name="connecting-oms-workspace-to-power-bi"></a><span data-ttu-id="91983-121">Подключение рабочей области OMS к Power BI</span><span class="sxs-lookup"><span data-stu-id="91983-121">Connecting OMS workspace to Power BI</span></span>
<span data-ttu-id="91983-122">Прежде чем экспортировать данные из службы Log Analytics в Power BI, необходимо подключить рабочую область OMS к учетной записи Power BI, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="91983-122">Before you can export from Log Analytics to Power BI, you must connect your OMS workspace to your Power BI account using the following procedure.</span></span>  

1. <span data-ttu-id="91983-123">В консоли OMS щелкните элемент **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="91983-123">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="91983-124">Выберите **Учетные записи**.</span><span class="sxs-lookup"><span data-stu-id="91983-124">Select **Accounts**.</span></span>
3. <span data-ttu-id="91983-125">В разделе **Сведения о рабочей области** щелкните **Подключиться к учетной записи Power BI**.</span><span class="sxs-lookup"><span data-stu-id="91983-125">In the **Workspace Information** section click **Connect to Power BI Account**.</span></span>
4. <span data-ttu-id="91983-126">Введите данные учетной записи Power BI.</span><span class="sxs-lookup"><span data-stu-id="91983-126">Enter the credentials for your Power BI account.</span></span>

## <a name="create-a-power-bi-schedule"></a><span data-ttu-id="91983-127">Создание расписания Power BI</span><span class="sxs-lookup"><span data-stu-id="91983-127">Create a Power BI Schedule</span></span>
<span data-ttu-id="91983-128">Создайте расписание Power BI для каждого набора данных, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="91983-128">Create a Power BI Schedule for each dataset using the following procedure.</span></span>

1. <span data-ttu-id="91983-129">В консоли OMS щелкните элемент **Поиск по журналам** .</span><span class="sxs-lookup"><span data-stu-id="91983-129">In the OMS console click the **Log Search** tile.</span></span>
2. <span data-ttu-id="91983-130">Введите новый запрос или выберите сохраненный поиск, возвращающий данные, которые нужно экспортировать в **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="91983-130">Type in a new query or select a saved search that returns the data that you want to export to **Power BI**.</span></span>  
3. <span data-ttu-id="91983-131">Нажмите кнопку **Power BI** в верхней части страницы, чтобы открыть диалоговое окно **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="91983-131">Click the **Power BI** button at the top of the page to open the **Power BI** dialog.</span></span>
4. <span data-ttu-id="91983-132">Введите данные в следующую таблицу и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="91983-132">Provide the information in the following table and click **Save**.</span></span>

| <span data-ttu-id="91983-133">Свойство</span><span class="sxs-lookup"><span data-stu-id="91983-133">Property</span></span> | <span data-ttu-id="91983-134">Описание</span><span class="sxs-lookup"><span data-stu-id="91983-134">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="91983-135">Действие</span><span class="sxs-lookup"><span data-stu-id="91983-135">Name</span></span> |<span data-ttu-id="91983-136">Имя для идентификации расписания при просмотре списка расписаний Power BI.</span><span class="sxs-lookup"><span data-stu-id="91983-136">Name to identify the schedule when you view the list of Power BI schedules.</span></span> |
| <span data-ttu-id="91983-137">Сохраненные поисковые запросы</span><span class="sxs-lookup"><span data-stu-id="91983-137">Saved Search</span></span> |<span data-ttu-id="91983-138">Поисковый запрос, который нужно выполнить.</span><span class="sxs-lookup"><span data-stu-id="91983-138">The log search to run.</span></span>  <span data-ttu-id="91983-139">Вы можете выбрать текущий запрос и сохраненный поисковый запрос из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="91983-139">You can either select the current query or select an existing saved search from the dropdown box.</span></span> |
| <span data-ttu-id="91983-140">Расписание</span><span class="sxs-lookup"><span data-stu-id="91983-140">Schedule</span></span> |<span data-ttu-id="91983-141">Периодичность выполнения сохраненного поискового запроса и экспорта в набор данных Power BI.</span><span class="sxs-lookup"><span data-stu-id="91983-141">How often to run the saved search and export to the Power BI dataset.</span></span>  <span data-ttu-id="91983-142">Значение должно составлять от 15 минут до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="91983-142">The value must be between 15 minutes and 24 hours.</span></span> |
| <span data-ttu-id="91983-143">Имя набора данных</span><span class="sxs-lookup"><span data-stu-id="91983-143">Dataset Name</span></span> |<span data-ttu-id="91983-144">Имя набора данных в Power BI.</span><span class="sxs-lookup"><span data-stu-id="91983-144">The name of the dataset in Power BI.</span></span>  <span data-ttu-id="91983-145">Если оно не существует, то создается, а если существует, то обновляется.</span><span class="sxs-lookup"><span data-stu-id="91983-145">It will be created if it doesn’t exist and updated if it does exist.</span></span> |

## <a name="viewing-and-removing-power-bi-schedules"></a><span data-ttu-id="91983-146">Просмотр и удаление расписаний Power BI</span><span class="sxs-lookup"><span data-stu-id="91983-146">Viewing and Removing Power BI Schedules</span></span>
<span data-ttu-id="91983-147">Просмотрите список существующих расписаний Power BI, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="91983-147">View the list of existing Power BI Schedules with the following procedure.</span></span>

1. <span data-ttu-id="91983-148">В консоли OMS щелкните элемент **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="91983-148">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="91983-149">Выберите **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="91983-149">Select **Power BI**.</span></span>

<span data-ttu-id="91983-150">Наряду с информацией о расписании отображаются данные о том, сколько раз расписание было выполнено за прошлую неделю, а также состояние последней синхронизации.</span><span class="sxs-lookup"><span data-stu-id="91983-150">In addition to the details of the schedule, the number of times that the schedule has run in the past week and the status of the last sync are displayed.</span></span>  <span data-ttu-id="91983-151">Если при синхронизации возникают ошибки, щелкните ссылку для поиска записей, содержащих сведения об ошибке, по журналам.</span><span class="sxs-lookup"><span data-stu-id="91983-151">If the sync encountered errors, you can click the link to run a log search for records with details of the error.</span></span>

<span data-ttu-id="91983-152">Расписание можно удалить, щелкнув **X** в столбце **Удалить столбец**.</span><span class="sxs-lookup"><span data-stu-id="91983-152">You can remove a schedule by clicking on the **X** in the **Remove column**.</span></span>  <span data-ttu-id="91983-153">Расписание можно отключить, выбрав параметр **Откл**.</span><span class="sxs-lookup"><span data-stu-id="91983-153">You can disable a schedule by selecting **Off**.</span></span>  <span data-ttu-id="91983-154">Чтобы изменить расписание, необходимо удалить его и создать новое с новыми параметрами.</span><span class="sxs-lookup"><span data-stu-id="91983-154">To modify a schedule you must remove it and recreate it with the new settings.</span></span>

![Расписания Power BI](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a><span data-ttu-id="91983-156">Пример пошагового руководства</span><span class="sxs-lookup"><span data-stu-id="91983-156">Sample walkthrough</span></span>
<span data-ttu-id="91983-157">В следующем разделе демонстрируется создание расписания Power BI и использование его набора данных для создания простого отчета.</span><span class="sxs-lookup"><span data-stu-id="91983-157">The following section walks through an example of creating a Power BI Schedule and using its dataset to create a simple report.</span></span>  <span data-ttu-id="91983-158">В этом примере все данные о производительности по набору компьютеров экспортируются в Power BI, после чего создается линейный график, который показывает загрузку процессора.</span><span class="sxs-lookup"><span data-stu-id="91983-158">In this example, all performance data for a set of computers is exported to Power BI and then a line graph is created to display processor utilization.</span></span>

### <a name="create-log-search"></a><span data-ttu-id="91983-159">Создание запроса поиска по журналу</span><span class="sxs-lookup"><span data-stu-id="91983-159">Create log search</span></span>
<span data-ttu-id="91983-160">Для начала создадим запрос для поиска данных, которые нужно отправить в набор данных.</span><span class="sxs-lookup"><span data-stu-id="91983-160">We start by creating a log search for the data that we want to send to the dataset.</span></span>  <span data-ttu-id="91983-161">В этом примере будет использоваться запрос, возвращающий все данные о производительности компьютеров, имена которых начинаются с *srv*.</span><span class="sxs-lookup"><span data-stu-id="91983-161">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span></span>  

![Расписания Power BI](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a><span data-ttu-id="91983-163">Создания запроса для поиска по Power BI</span><span class="sxs-lookup"><span data-stu-id="91983-163">Create Power BI Search</span></span>
<span data-ttu-id="91983-164">Мы нажимаем кнопку **Power BI** , чтобы открыть диалоговое окно Power BI и ввести необходимые данные.</span><span class="sxs-lookup"><span data-stu-id="91983-164">We click the **Power BI** button to open the Power BI dialog and provide the required information.</span></span>  <span data-ttu-id="91983-165">Мы хотим, чтобы этот поиск выполнялся один раз в час и создавал набор данных с именем *Contoso Perf*.</span><span class="sxs-lookup"><span data-stu-id="91983-165">We want this search to run once per hour and create a dataset called *Contoso Perf*.</span></span>  <span data-ttu-id="91983-166">Так как у нас уже есть поисковый запрос, выдающий необходимые данные, для параметра *Сохраненный поисковый запрос* мы оставляем значение по умолчанию **Использовать текущий поисковый запрос**.</span><span class="sxs-lookup"><span data-stu-id="91983-166">Since we already have the search open that creates the data we want, we keep the default of *Use current search query* for **Saved Search**.</span></span>

![Поиск Power BI](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a><span data-ttu-id="91983-168">Проверка поиска по Power BI</span><span class="sxs-lookup"><span data-stu-id="91983-168">Verify Power BI Search</span></span>
<span data-ttu-id="91983-169">Чтобы проверить, правильно ли создано расписание, мы просматриваем список поисковых запросов Power BI в элементе **Параметры** на панели мониторинга OMS.</span><span class="sxs-lookup"><span data-stu-id="91983-169">To verify that we created the schedule correctly, we view the list of Power BI Searches under the **Settings** tile in the OMS dashboard.</span></span>  <span data-ttu-id="91983-170">Мы ждем несколько минут и обновляем представление, пока оно не сообщит, что синхронизация выполнена.</span><span class="sxs-lookup"><span data-stu-id="91983-170">We wait several minutes and refresh this view until it reports that the sync has been run.</span></span>

![Поиск Power BI](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-the-dataset-in-power-bi"></a><span data-ttu-id="91983-172">Проверка набора данных в Power BI</span><span class="sxs-lookup"><span data-stu-id="91983-172">Verify the dataset in Power BI</span></span>
<span data-ttu-id="91983-173">Мы входим в свою учетную запись на сайте [powerbi.microsoft.com](http://powerbi.microsoft.com/) и прокручиваем экран до пункта **Datasets** (Наборы данных) в нижней части левой панели.</span><span class="sxs-lookup"><span data-stu-id="91983-173">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll to **Datasets** at the bottom of the left pane.</span></span>  <span data-ttu-id="91983-174">Как видите, набор данных *Contoso Perf* присутствует в списке с указанием на то, что экспорт был выполнен успешно.</span><span class="sxs-lookup"><span data-stu-id="91983-174">We can see that the *Contoso Perf* dataset is listed indicating that our export has run successfully.</span></span>

![Набор данных Power BI](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a><span data-ttu-id="91983-176">Создание отчета на основе набора данных</span><span class="sxs-lookup"><span data-stu-id="91983-176">Create report based on dataset</span></span>
<span data-ttu-id="91983-177">Мы выбираем набор данных **Contoso Perf** и щелкаем **Results** (Результат) на панели **Fields** (Поля) справа, чтобы просмотреть, какие поля входят в этот набор данных.</span><span class="sxs-lookup"><span data-stu-id="91983-177">We select the **Contoso Perf** dataset and then click on **Results** in the **Fields** pane on the right to view the fields that are part of this dataset.</span></span>  <span data-ttu-id="91983-178">Чтобы создать линейный график, отражающий использование процессора на каждом компьютере, мы выполняем следующие действия:</span><span class="sxs-lookup"><span data-stu-id="91983-178">To create a line graph showing processor utilization for each computer, we perform the following actions.</span></span>

1. <span data-ttu-id="91983-179">Выбираем визуализацию линейного графика.</span><span class="sxs-lookup"><span data-stu-id="91983-179">Select the Line chart visualization.</span></span>
2. <span data-ttu-id="91983-180">Перетаскиваем параметр **ObjectName** (Имя объекта) в **Report level filter** (Фильтр уровней отчетности) и устанавливаем флажок **Processor** (Процесс).</span><span class="sxs-lookup"><span data-stu-id="91983-180">Drag **ObjectName** to **Report level filter** and check **Processor**.</span></span>
3. <span data-ttu-id="91983-181">Перетаскиваем параметр **CounterName** (Имя счетчика) в **Report level filter** (Фильтр уровней отчетности) и устанавливаем флажок **% Processor Time** (Процент процессорного времени).</span><span class="sxs-lookup"><span data-stu-id="91983-181">Drag **CounterName** to **Report level filter** and check **% Processor Time**.</span></span>
4. <span data-ttu-id="91983-182">Перетаскиваем параметр **CounterValue** (Значение счетчика) в поле **Values** (Значения).</span><span class="sxs-lookup"><span data-stu-id="91983-182">Drag **CounterValue** to **Values**.</span></span>
5. <span data-ttu-id="91983-183">Перетаскиваем параметр **Computer** (Компьютер) в поле **Legend** (Условные обозначения).</span><span class="sxs-lookup"><span data-stu-id="91983-183">Drag **Computer** to **Legend**.</span></span>
6. <span data-ttu-id="91983-184">Перетаскиваем параметр **TimeGenerated** (Время создания) в поле **Axis** (Ось).</span><span class="sxs-lookup"><span data-stu-id="91983-184">Drag **TimeGenerated** to **Axis**.</span></span>

<span data-ttu-id="91983-185">В результате отображается линейный график с данными из набора данных.</span><span class="sxs-lookup"><span data-stu-id="91983-185">We can see that the resulting line graph is displayed with the data from our dataset.</span></span>

![График Power BI](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-the-report"></a><span data-ttu-id="91983-187">Сохранение отчета</span><span class="sxs-lookup"><span data-stu-id="91983-187">Save the report</span></span>
<span data-ttu-id="91983-188">Мы сохраняем отчет, нажав кнопку "Сохранить" в верхней части экрана, и проверяем, отображается ли он в разделе Report (Отчет) на левой панели.</span><span class="sxs-lookup"><span data-stu-id="91983-188">We save the report by clicking on the Save button at the top of the screen and validate that it is now listed in the Reports section in the left pane.</span></span>

![Отчеты Power BI](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a><span data-ttu-id="91983-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="91983-190">Next steps</span></span>
* <span data-ttu-id="91983-191">Узнайте больше о [запросах поиска по журналам](log-analytics-log-searches.md) , чтобы создавать запросы, которые можно экспортировать в Power BI.</span><span class="sxs-lookup"><span data-stu-id="91983-191">Learn about [log searches](log-analytics-log-searches.md) to build queries that can be exported to Power BI.</span></span>
* <span data-ttu-id="91983-192">Узнайте больше о [Power BI](http://powerbi.microsoft.com), чтобы создавать визуализации на основе экспорта Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="91983-192">Learn more about [Power BI](http://powerbi.microsoft.com) to build visualizations based on Log Analytics exports.</span></span>
