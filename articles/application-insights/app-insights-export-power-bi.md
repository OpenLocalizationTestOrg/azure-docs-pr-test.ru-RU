---
title: "Экспорт в Power BI из Application Insights | Документация Майкрософт"
description: "Аналитические запросы можно просматривать в Power BI."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 350a65b1c6432baf258e014c9e63133d2b29e34f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="0378d-103">Использование данных Application Insights в Power BI</span><span class="sxs-lookup"><span data-stu-id="0378d-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="0378d-104">[Power BI](http://www.powerbi.com/) — это набор средств бизнес-аналитики для анализа данных и обмена сведениями.</span><span class="sxs-lookup"><span data-stu-id="0378d-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="0378d-105">На каждом устройстве доступны панели мониторинга с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="0378d-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="0378d-106">Вы можете объединять данные из различных источников, в том числе аналитические запросы из [ Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0378d-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="0378d-107">Существуют три рекомендуемых способа экспортировать данные Application Insights в Power BI.</span><span class="sxs-lookup"><span data-stu-id="0378d-107">There are three recommended methods of exporting Application Insights data to Power BI.</span></span> <span data-ttu-id="0378d-108">Их можно использовать отдельно или совместно.</span><span class="sxs-lookup"><span data-stu-id="0378d-108">You can use them separately or together.</span></span>

* <span data-ttu-id="0378d-109">[**Использование адаптера Power BI** ](#power-pi-adapter). С его помощью можно настроить панель мониторинга телеметрии из своего приложения.</span><span class="sxs-lookup"><span data-stu-id="0378d-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="0378d-110">Здесь есть предопределенный набор диаграмм, но можно добавлять свои запросы из других источников.</span><span class="sxs-lookup"><span data-stu-id="0378d-110">The set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="0378d-111">[**Экспорт аналитических запросов**](#export-analytics-queries). Напишите необходимый запрос с помощью средства аналитики и экспортируйте этот запрос в Power BI.</span><span class="sxs-lookup"><span data-stu-id="0378d-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it to Power BI.</span></span> <span data-ttu-id="0378d-112">Его можно разместить на панели мониторинга вместе с другими данными.</span><span class="sxs-lookup"><span data-stu-id="0378d-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="0378d-113">[**Непрерывный экспорт и Stream Analytics.**](app-insights-export-stream-analytics.md) Это самый трудоемкий метод.</span><span class="sxs-lookup"><span data-stu-id="0378d-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work to set up.</span></span> <span data-ttu-id="0378d-114">Он полезен, если необходимо хранить данные в течение долгого времени.</span><span class="sxs-lookup"><span data-stu-id="0378d-114">It is useful if you want to keep your data for long periods.</span></span> <span data-ttu-id="0378d-115">В иных случаях рекомендуется использовать другие методы.</span><span class="sxs-lookup"><span data-stu-id="0378d-115">Otherwise, the other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="0378d-116">Использование адаптера Power BI</span><span class="sxs-lookup"><span data-stu-id="0378d-116">Power BI adapter</span></span>
<span data-ttu-id="0378d-117">Этот метод предполагает создание панели мониторинга телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0378d-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="0378d-118">Предусматривается первоначальный набор данных, но к нему можно добавлять больше сведений.</span><span class="sxs-lookup"><span data-stu-id="0378d-118">The initial data set is predefined, but you can add more data to it.</span></span>

### <a name="get-the-adapter"></a><span data-ttu-id="0378d-119">Получение адаптера</span><span class="sxs-lookup"><span data-stu-id="0378d-119">Get the adapter</span></span>
1. <span data-ttu-id="0378d-120">Войдите в [Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="0378d-120">Sign in to [Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="0378d-121">Выберите **Получение данных**, **Службы**, **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="0378d-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Получение из источника данных Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="0378d-123">Укажите сведения о ресурсе Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0378d-123">Provide the details of your Application Insights resource.</span></span>
   
    ![Получение из источника данных Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="0378d-125">Дождитесь завершения импорта данных.</span><span class="sxs-lookup"><span data-stu-id="0378d-125">Wait a minute or two for the data to be imported.</span></span>
   
    ![Использование адаптера Power BI](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="0378d-127">Панель мониторинга можно настраивать, объединяя диаграммы Application Insights с диаграммами из других источников и с аналитическими запросами.</span><span class="sxs-lookup"><span data-stu-id="0378d-127">You can edit the dashboard, combining the Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="0378d-128">В коллекции визуализации доступны дополнительные диаграммы, и у каждой диаграммы есть параметры, которые можно задать.</span><span class="sxs-lookup"><span data-stu-id="0378d-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="0378d-129">После первоначального импорта панель мониторинга и отчеты продолжают обновляться ежедневно.</span><span class="sxs-lookup"><span data-stu-id="0378d-129">After the initial import, the dashboard and the reports continue to update daily.</span></span> <span data-ttu-id="0378d-130">При этом можно управлять расписанием обновления для набора данных.</span><span class="sxs-lookup"><span data-stu-id="0378d-130">You can control the refresh schedule on the dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="0378d-131">Экспорт запросов аналитики</span><span class="sxs-lookup"><span data-stu-id="0378d-131">Export Analytics queries</span></span>
<span data-ttu-id="0378d-132">Этот способ предполагает написание любого аналитического запроса, а затем его экспорт на панель мониторинга Power BI.</span><span class="sxs-lookup"><span data-stu-id="0378d-132">This route allows you to write any Analytics query you like, and then export that to a Power BI dashboard.</span></span> <span data-ttu-id="0378d-133">(Его можно добавить на панель мониторинга, созданную при помощи адаптера.)</span><span class="sxs-lookup"><span data-stu-id="0378d-133">(You can add to the dashboard created by the adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="0378d-134">Короткий путь: установка Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="0378d-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="0378d-135">Чтобы импортировать запрос Application Insights, используйте версию Power BI для компьютера.</span><span class="sxs-lookup"><span data-stu-id="0378d-135">To import your Application Insights query, you use the desktop version of Power BI.</span></span> <span data-ttu-id="0378d-136">Затем запрос можно опубликовать в Интернете или в рабочей области облака Power BI.</span><span class="sxs-lookup"><span data-stu-id="0378d-136">But then you can publish it to the web or to your Power BI cloud workspace.</span></span> 

<span data-ttu-id="0378d-137">Установите [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="0378d-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="0378d-138">Экспорт запроса аналитики</span><span class="sxs-lookup"><span data-stu-id="0378d-138">Export an Analytics query</span></span>
1. <span data-ttu-id="0378d-139">[Откройте средство аналитики и напишите запрос](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="0378d-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="0378d-140">Протестируйте запрос и откорректируйте его до необходимой степени.</span><span class="sxs-lookup"><span data-stu-id="0378d-140">Test and refine the query until you're happy with the results.</span></span>

   <span data-ttu-id="0378d-141">**Прежде чем экспортировать запрос, убедитесь, что он выполняется в Analytics надлежащим образом.**</span><span class="sxs-lookup"><span data-stu-id="0378d-141">**Make sure that the query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="0378d-142">В меню **Export** (Экспорт) выберите пункт **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="0378d-142">On the **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="0378d-143">Сохраните текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="0378d-143">Save the text file.</span></span>
   
    ![Экспорт запроса Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="0378d-145">В Power BI Desktop выберите меню **Get Data, Blank Query** (Получить данные, пустой запрос), а затем в редакторе запросов на вкладке **Представление** выберите **расширенный редактор запросов**.</span><span class="sxs-lookup"><span data-stu-id="0378d-145">In Power BI Desktop select **Get Data, Blank Query** and then in the query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="0378d-146">Вставьте скрипт на языке M в расширенный редактор запросов.</span><span class="sxs-lookup"><span data-stu-id="0378d-146">Paste the exported M Language script into the Advanced Query Editor.</span></span>

    ![Расширенный редактор запросов](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="0378d-148">Чтобы разрешить Power BI доступ к Azure, может потребоваться указать учетные данные.</span><span class="sxs-lookup"><span data-stu-id="0378d-148">You might have to provide credentials to allow Power BI to access Azure.</span></span> <span data-ttu-id="0378d-149">Щелкните "Учетная запись организации", чтобы войти, используя свою учетную запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0378d-149">Use 'organizational account' to sign in with your Microsoft account.</span></span>
   
    ![Укажите учетные данные Azure, чтобы Power BI выполнила запрос Application Insights.](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="0378d-151">(Если нужно проверить учетные данные, используйте команду меню "Параметры источника данных" в редакторе запросов.</span><span class="sxs-lookup"><span data-stu-id="0378d-151">(If you need to verify the credentials, use the Data Source Settings menu command in the Query Editor.</span></span> <span data-ttu-id="0378d-152">Укажите учетные данные, используемые для Azure. Они могут отличаться от учетных данных для Power BI.)</span><span class="sxs-lookup"><span data-stu-id="0378d-152">Take care to specify the credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="0378d-153">Выберите визуализацию для запроса, измерение сегментирования, поля для осей X и Y.</span><span class="sxs-lookup"><span data-stu-id="0378d-153">Choose a visualization for your query and select the fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Выбор визуализации](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="0378d-155">Опубликуйте отчет в рабочей области облака Power BI.</span><span class="sxs-lookup"><span data-stu-id="0378d-155">Publish your report to your Power BI cloud workspace.</span></span> <span data-ttu-id="0378d-156">Из нее можно внедрять синхронизированную версию на другие веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="0378d-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Выбор визуализации](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="0378d-158">Периодически обновляйте отчет вручную или настройте запланированное обновление на странице параметров.</span><span class="sxs-lookup"><span data-stu-id="0378d-158">Refresh the report manually at intervals, or set up a scheduled refresh on the options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0378d-159">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="0378d-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="0378d-160">401 или 403 — недостаточно прав</span><span class="sxs-lookup"><span data-stu-id="0378d-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="0378d-161">Это может произойти, если токен обновления не обновлен.</span><span class="sxs-lookup"><span data-stu-id="0378d-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="0378d-162">Попробуйте выполнить следующие действия, чтобы убедиться, что у вас по-прежнему есть доступ.</span><span class="sxs-lookup"><span data-stu-id="0378d-162">Try these steps to ensure you still have access.</span></span> <span data-ttu-id="0378d-163">Если у вас есть доступ, но обновление учетных данных не работает, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="0378d-163">If you do have access and refershing the credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="0378d-164">Войдите на портал Azure и убедитесь, что можете получить доступ к ресурсу.</span><span class="sxs-lookup"><span data-stu-id="0378d-164">Log into the Azure Portal and make sure you can access the resource</span></span>
2. <span data-ttu-id="0378d-165">Попробуйте обновить учетные данные для панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="0378d-165">Try to refresh the credentials for the Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="0378d-166">502 — Недопустимый шлюз</span><span class="sxs-lookup"><span data-stu-id="0378d-166">502 Bad Gateway</span></span>
<span data-ttu-id="0378d-167">Обычно это вызвано запросом аналитики, который возвращает слишком много данных.</span><span class="sxs-lookup"><span data-stu-id="0378d-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="0378d-168">Вначале следует попробовать использовать меньший диапазон времени или использовать функции [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) или [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) только для необходимых полей [проекта](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator).</span><span class="sxs-lookup"><span data-stu-id="0378d-168">You should try using a smaller time range or by using the [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) the fields you need.</span></span>

<span data-ttu-id="0378d-169">Если уменьшение набора данных, поступающих от запросов аналитики, не соответствует вашим требованиям, можно использовать [API](https://dev.applicationinsights.io/documentation/overview) для извлечения набора данных большего размера.</span><span class="sxs-lookup"><span data-stu-id="0378d-169">If reducing the dataset coming from the Analytics query doesn't meet your requirements you should consider using the [API](https://dev.applicationinsights.io/documentation/overview) to pull a larger dataset.</span></span> <span data-ttu-id="0378d-170">Ниже приведены инструкции по преобразованию экспорта запросов на языке M для использования API.</span><span class="sxs-lookup"><span data-stu-id="0378d-170">Here are instructions on how to convert the M-Query export to use the API.</span></span>

1. <span data-ttu-id="0378d-171">Создайте [ключ API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID).</span><span class="sxs-lookup"><span data-stu-id="0378d-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="0378d-172">Обновите скрипт Power BI на языке M, экспортированный из аналитики, заменив URL-адрес ARM на API AI (см. пример ниже).</span><span class="sxs-lookup"><span data-stu-id="0378d-172">Update the Power BI M script that you exported from Analytics by replacing the ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="0378d-173">Замените **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="0378d-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="0378d-174">на **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="0378d-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="0378d-175">Наконец, обновите учетные данные на базовые и используйте ваш ключ API.</span><span class="sxs-lookup"><span data-stu-id="0378d-175">Finally, update credentials to basic, and use your API Key</span></span>
  

<span data-ttu-id="0378d-176">**Существующий скрипт**</span><span class="sxs-lookup"><span data-stu-id="0378d-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="0378d-177">**Обновленный скрипт**</span><span class="sxs-lookup"><span data-stu-id="0378d-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="0378d-178">Дополнительная информация о выборке</span><span class="sxs-lookup"><span data-stu-id="0378d-178">About sampling</span></span>
<span data-ttu-id="0378d-179">Если ваше приложение отправляет большие объемы данных, может сработать функция адаптивной выборки и отправить только часть вашей телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0378d-179">If your application sends a lot of data, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="0378d-180">То же произойдет, если выборка настроена вручную в пакете SDK или на приеме.</span><span class="sxs-lookup"><span data-stu-id="0378d-180">The same is true if you have manually set sampling either in the SDK or on ingestion.</span></span> [<span data-ttu-id="0378d-181">Дополнительная информация о выборке.</span><span class="sxs-lookup"><span data-stu-id="0378d-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="0378d-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0378d-182">Next steps</span></span>
* [<span data-ttu-id="0378d-183">Дополнительные сведения о Power BI</span><span class="sxs-lookup"><span data-stu-id="0378d-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="0378d-184">Руководство по аналитике</span><span class="sxs-lookup"><span data-stu-id="0378d-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

