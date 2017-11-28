---
title: "tooPower aaaExport бизнес-Аналитики из Application Insights | Документы Microsoft"
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
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="0ed39-103">Использование данных Application Insights в Power BI</span><span class="sxs-lookup"><span data-stu-id="0ed39-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="0ed39-104">[Power BI](http://www.powerbi.com/) — это набор средств бизнес-аналитики для анализа данных и обмена сведениями.</span><span class="sxs-lookup"><span data-stu-id="0ed39-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="0ed39-105">На каждом устройстве доступны панели мониторинга с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="0ed39-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="0ed39-106">Вы можете объединять данные из различных источников, в том числе аналитические запросы из [ Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ed39-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="0ed39-107">Существуют три способа рекомендуемые экспорта tooPower Application Insights данных бизнес-Аналитики.</span><span class="sxs-lookup"><span data-stu-id="0ed39-107">There are three recommended methods of exporting Application Insights data tooPower BI.</span></span> <span data-ttu-id="0ed39-108">Их можно использовать отдельно или совместно.</span><span class="sxs-lookup"><span data-stu-id="0ed39-108">You can use them separately or together.</span></span>

* <span data-ttu-id="0ed39-109">[**Использование адаптера Power BI** ](#power-pi-adapter). С его помощью можно настроить панель мониторинга телеметрии из своего приложения.</span><span class="sxs-lookup"><span data-stu-id="0ed39-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="0ed39-110">предопределенные Hello набора диаграмм, но можно добавить собственные запросы с другими источниками.</span><span class="sxs-lookup"><span data-stu-id="0ed39-110">hello set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="0ed39-111">[**Экспорт аналитические запросы** ](#export-analytics-queries) -записи любого запроса с помощью аналитика и экспортировать его tooPower бизнес-Аналитики.</span><span class="sxs-lookup"><span data-stu-id="0ed39-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it tooPower BI.</span></span> <span data-ttu-id="0ed39-112">Его можно разместить на панели мониторинга вместе с другими данными.</span><span class="sxs-lookup"><span data-stu-id="0ed39-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="0ed39-113">[**Непрерывный Экспорт и Stream Analytics** ](app-insights-export-stream-analytics.md) -это включает в себя дополнительные рабочие tooset вверх.</span><span class="sxs-lookup"><span data-stu-id="0ed39-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work tooset up.</span></span> <span data-ttu-id="0ed39-114">Оно полезно в том случае, если требуется tookeep данных для длительных периодов времени.</span><span class="sxs-lookup"><span data-stu-id="0ed39-114">It is useful if you want tookeep your data for long periods.</span></span> <span data-ttu-id="0ed39-115">В противном случае hello других методов, рекомендуется использовать.</span><span class="sxs-lookup"><span data-stu-id="0ed39-115">Otherwise, hello other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="0ed39-116">Использование адаптера Power BI</span><span class="sxs-lookup"><span data-stu-id="0ed39-116">Power BI adapter</span></span>
<span data-ttu-id="0ed39-117">Этот метод предполагает создание панели мониторинга телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0ed39-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="0ed39-118">предопределенные Hello первоначального набора данных, но можно добавить дополнительные tooit данных.</span><span class="sxs-lookup"><span data-stu-id="0ed39-118">hello initial data set is predefined, but you can add more data tooit.</span></span>

### <a name="get-hello-adapter"></a><span data-ttu-id="0ed39-119">Получает адаптер hello</span><span class="sxs-lookup"><span data-stu-id="0ed39-119">Get hello adapter</span></span>
1. <span data-ttu-id="0ed39-120">Войдите в слишком[Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="0ed39-120">Sign in too[Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="0ed39-121">Выберите **Получение данных**, **Службы**, **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="0ed39-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Получение из источника данных Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="0ed39-123">Подробно hello ресурса Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0ed39-123">Provide hello details of your Application Insights resource.</span></span>
   
    ![Получение из источника данных Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="0ed39-125">Подождите одну или две для импорта toobe данных hello минуты.</span><span class="sxs-lookup"><span data-stu-id="0ed39-125">Wait a minute or two for hello data toobe imported.</span></span>
   
    ![Использование адаптера Power BI](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="0ed39-127">Можно изменить панель мониторинга hello, объединение диаграмм hello Application Insights с их из других источников и аналитические запросы.</span><span class="sxs-lookup"><span data-stu-id="0ed39-127">You can edit hello dashboard, combining hello Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="0ed39-128">В коллекции визуализации доступны дополнительные диаграммы, и у каждой диаграммы есть параметры, которые можно задать.</span><span class="sxs-lookup"><span data-stu-id="0ed39-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="0ed39-129">После первоначального импорта hello, hello панели мониторинга и отчеты hello продолжить tooupdate ежедневно.</span><span class="sxs-lookup"><span data-stu-id="0ed39-129">After hello initial import, hello dashboard and hello reports continue tooupdate daily.</span></span> <span data-ttu-id="0ed39-130">Можно управлять hello расписание обновления для набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="0ed39-130">You can control hello refresh schedule on hello dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="0ed39-131">Экспорт запросов аналитики</span><span class="sxs-lookup"><span data-stu-id="0ed39-131">Export Analytics queries</span></span>
<span data-ttu-id="0ed39-132">Данный маршрут позволяет toowrite любой Analytics вы хотите запросить, а затем экспортируйте этой панели мониторинга Power BI tooa.</span><span class="sxs-lookup"><span data-stu-id="0ed39-132">This route allows you toowrite any Analytics query you like, and then export that tooa Power BI dashboard.</span></span> <span data-ttu-id="0ed39-133">(Можно добавить toohello панель мониторинга, созданную адаптером hello.)</span><span class="sxs-lookup"><span data-stu-id="0ed39-133">(You can add toohello dashboard created by hello adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="0ed39-134">Короткий путь: установка Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="0ed39-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="0ed39-135">tooimport запроса Application Insights, используйте Power BI версии hello настольного компьютера.</span><span class="sxs-lookup"><span data-stu-id="0ed39-135">tooimport your Application Insights query, you use hello desktop version of Power BI.</span></span> <span data-ttu-id="0ed39-136">Но затем его можно опубликовать веб-toohello или tooyour рабочей области Power BI облака.</span><span class="sxs-lookup"><span data-stu-id="0ed39-136">But then you can publish it toohello web or tooyour Power BI cloud workspace.</span></span> 

<span data-ttu-id="0ed39-137">Установите [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="0ed39-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="0ed39-138">Экспорт запроса аналитики</span><span class="sxs-lookup"><span data-stu-id="0ed39-138">Export an Analytics query</span></span>
1. <span data-ttu-id="0ed39-139">[Откройте средство аналитики и напишите запрос](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="0ed39-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="0ed39-140">Тестирование и доработку hello запроса, пока вы довольны hello результаты.</span><span class="sxs-lookup"><span data-stu-id="0ed39-140">Test and refine hello query until you're happy with hello results.</span></span>

   <span data-ttu-id="0ed39-141">**Убедитесь, что hello запросов выполняется правильно в аналитике, прежде чем экспортировать его.**</span><span class="sxs-lookup"><span data-stu-id="0ed39-141">**Make sure that hello query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="0ed39-142">На hello **Экспорт** меню, выберите **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="0ed39-142">On hello **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="0ed39-143">Сохраните текстовый файл hello.</span><span class="sxs-lookup"><span data-stu-id="0ed39-143">Save hello text file.</span></span>
   
    ![Экспорт запроса Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="0ed39-145">В Power BI Desktop выберите **получить данные, пустой запрос** и затем в hello редактор запросов, в разделе **представление** выберите **расширенного редактора запросов**.</span><span class="sxs-lookup"><span data-stu-id="0ed39-145">In Power BI Desktop select **Get Data, Blank Query** and then in hello query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="0ed39-146">Вставить скрипт язык M hello экспортированы в hello расширенного редактора запросов.</span><span class="sxs-lookup"><span data-stu-id="0ed39-146">Paste hello exported M Language script into hello Advanced Query Editor.</span></span>

    ![Расширенный редактор запросов](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="0ed39-148">Может потребоваться Power BI-tooaccess tooallow tooprovide учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="0ed39-148">You might have tooprovide credentials tooallow Power BI tooaccess Azure.</span></span> <span data-ttu-id="0ed39-149">Используйте «учетная запись организации» toosign учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0ed39-149">Use 'organizational account' toosign in with your Microsoft account.</span></span>
   
    ![Укажите учетные данные Azure tooenable Power BI toorun запроса Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="0ed39-151">(Если необходимы учетные данные tooverify hello, используйте команду меню hello параметры источника данных в hello редактора запросов.</span><span class="sxs-lookup"><span data-stu-id="0ed39-151">(If you need tooverify hello credentials, use hello Data Source Settings menu command in hello Query Editor.</span></span> <span data-ttu-id="0ed39-152">Быть меры предосторожности hello toospecify учетные данные, которые для Azure, который может отличаться от учетных данных для Power BI.)</span><span class="sxs-lookup"><span data-stu-id="0ed39-152">Take care toospecify hello credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="0ed39-153">Выбрать визуализацию для запроса и выбирать поля hello для оси x, y и сегментирования измерения.</span><span class="sxs-lookup"><span data-stu-id="0ed39-153">Choose a visualization for your query and select hello fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Выбор визуализации](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="0ed39-155">Публикация отчетов Power BI tooyour облака рабочей области.</span><span class="sxs-lookup"><span data-stu-id="0ed39-155">Publish your report tooyour Power BI cloud workspace.</span></span> <span data-ttu-id="0ed39-156">Из нее можно внедрять синхронизированную версию на другие веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="0ed39-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Выбор визуализации](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="0ed39-158">Вручную обновить отчет hello интервалы или настроить запланированное обновление на странице параметров hello.</span><span class="sxs-lookup"><span data-stu-id="0ed39-158">Refresh hello report manually at intervals, or set up a scheduled refresh on hello options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0ed39-159">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="0ed39-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="0ed39-160">401 или 403 — недостаточно прав</span><span class="sxs-lookup"><span data-stu-id="0ed39-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="0ed39-161">Это может произойти, если токен обновления не обновлен.</span><span class="sxs-lookup"><span data-stu-id="0ed39-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="0ed39-162">Повторите эти шаги tooensure, по-прежнему имеется доступ.</span><span class="sxs-lookup"><span data-stu-id="0ed39-162">Try these steps tooensure you still have access.</span></span> <span data-ttu-id="0ed39-163">Если у вас есть доступ, и учетные данные обновлении hello не работает, обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="0ed39-163">If you do have access and refershing hello credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="0ed39-164">Войдите в портал Azure hello и убедитесь, что вам разрешен доступ к ресурсу hello</span><span class="sxs-lookup"><span data-stu-id="0ed39-164">Log into hello Azure Portal and make sure you can access hello resource</span></span>
2. <span data-ttu-id="0ed39-165">Попробуйте вводить учетные данные hello toorefresh для hello панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="0ed39-165">Try toorefresh hello credentials for hello Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="0ed39-166">502 — Недопустимый шлюз</span><span class="sxs-lookup"><span data-stu-id="0ed39-166">502 Bad Gateway</span></span>
<span data-ttu-id="0ed39-167">Обычно это вызвано запросом аналитики, который возвращает слишком много данных.</span><span class="sxs-lookup"><span data-stu-id="0ed39-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="0ed39-168">Вначале следует проверить с помощью меньший диапазон времени или с помощью hello [Назад](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) или [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) только для функций [проекта](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello необходимые поля.</span><span class="sxs-lookup"><span data-stu-id="0ed39-168">You should try using a smaller time range or by using hello [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello fields you need.</span></span>

<span data-ttu-id="0ed39-169">Если уменьшить hello набора данных, поступающих от hello аналитический запрос не соответствует вашим требованиям можно использовать hello [API](https://dev.applicationinsights.io/documentation/overview) toopull набора данных большего размера.</span><span class="sxs-lookup"><span data-stu-id="0ed39-169">If reducing hello dataset coming from hello Analytics query doesn't meet your requirements you should consider using hello [API](https://dev.applicationinsights.io/documentation/overview) toopull a larger dataset.</span></span> <span data-ttu-id="0ed39-170">Ниже приведены инструкции по инструкции tooconvert hello запросов M Экспорт toouse hello API.</span><span class="sxs-lookup"><span data-stu-id="0ed39-170">Here are instructions on how tooconvert hello M-Query export toouse hello API.</span></span>

1. <span data-ttu-id="0ed39-171">Создайте [ключ API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID).</span><span class="sxs-lookup"><span data-stu-id="0ed39-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="0ed39-172">Обновление hello Power BI M скрипт, который был экспортирован из Analytics, заменив hello ARM URL-адрес с AI API (см. пример ниже)</span><span class="sxs-lookup"><span data-stu-id="0ed39-172">Update hello Power BI M script that you exported from Analytics by replacing hello ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="0ed39-173">Замените **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="0ed39-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="0ed39-174">на **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="0ed39-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="0ed39-175">Наконец обновления toobasic учетные данные и использовать ваш ключ API</span><span class="sxs-lookup"><span data-stu-id="0ed39-175">Finally, update credentials toobasic, and use your API Key</span></span>
  

<span data-ttu-id="0ed39-176">**Существующий скрипт**</span><span class="sxs-lookup"><span data-stu-id="0ed39-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="0ed39-177">**Обновленный скрипт**</span><span class="sxs-lookup"><span data-stu-id="0ed39-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="0ed39-178">Дополнительная информация о выборке</span><span class="sxs-lookup"><span data-stu-id="0ed39-178">About sampling</span></span>
<span data-ttu-id="0ed39-179">Если приложение отправляет большой объем данных, функция адаптивной выборки hello может работать и отправьте доля телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0ed39-179">If your application sends a lot of data, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="0ed39-180">то же верно, если вручную выборки в hello SDK или на приема приветствия.</span><span class="sxs-lookup"><span data-stu-id="0ed39-180">hello same is true if you have manually set sampling either in hello SDK or on ingestion.</span></span> [<span data-ttu-id="0ed39-181">Дополнительная информация о выборке.</span><span class="sxs-lookup"><span data-stu-id="0ed39-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="0ed39-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0ed39-182">Next steps</span></span>
* [<span data-ttu-id="0ed39-183">Дополнительные сведения о Power BI</span><span class="sxs-lookup"><span data-stu-id="0ed39-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="0ed39-184">Руководство по аналитике</span><span class="sxs-lookup"><span data-stu-id="0ed39-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

