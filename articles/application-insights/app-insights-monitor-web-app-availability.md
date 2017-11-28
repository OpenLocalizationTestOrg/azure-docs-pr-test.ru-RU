---
title: "Наблюдение за доступностью и скоростью реагирования веб-сайта | Документация Майкрософт"
description: "Настройка веб-тестов в Application Insights. Получение оповещений, когда веб-сайт становится недоступным или медленно реагирует на запросы."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 6c7f52fc3998b0b29301206ffbc6a5a0c4134f6a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a><span data-ttu-id="b57ef-104">Наблюдение за доступностью и скоростью реагирования веб-сайта</span><span class="sxs-lookup"><span data-stu-id="b57ef-104">Monitor availability and responsiveness of any web site</span></span>
<span data-ttu-id="b57ef-105">Развернув веб-приложение или веб-сайт на любом сервере, вы можете настроить тесты для наблюдения за его доступностью и скоростью реагирования.</span><span class="sxs-lookup"><span data-stu-id="b57ef-105">After you've deployed your web app or web site to any server, you can set up tests to monitor its availability and responsiveness.</span></span> <span data-ttu-id="b57ef-106">[Azure Application Insights](app-insights-overview.md) отправляет веб-запросы через одинаковые промежутки времени из разных точек по всему миру.</span><span class="sxs-lookup"><span data-stu-id="b57ef-106">[Azure Application Insights](app-insights-overview.md) sends web requests to your application at regular intervals from points around the world.</span></span> <span data-ttu-id="b57ef-107">Эта надстройка предупреждает вас, если приложение реагирует медленно или не реагирует вообще.</span><span class="sxs-lookup"><span data-stu-id="b57ef-107">It alerts you if your application doesn't respond, or responds slowly.</span></span>

<span data-ttu-id="b57ef-108">Вы можете настроить тесты доступности для любой конечной точки HTTP или HTTPS, доступной из Интернета.</span><span class="sxs-lookup"><span data-stu-id="b57ef-108">You can set up availability tests for any HTTP or HTTPS endpoint that is accessible from the public internet.</span></span> <span data-ttu-id="b57ef-109">На тестируемый веб-сайт не нужно ничего добавлять.</span><span class="sxs-lookup"><span data-stu-id="b57ef-109">You don't have to add anything to the web site you're testing.</span></span> <span data-ttu-id="b57ef-110">Этот сайт даже может принадлежать кому-то другому. Вы можете протестировать службу REST API, от которой зависит ваш сайт.</span><span class="sxs-lookup"><span data-stu-id="b57ef-110">It doesn't even have to be your site: you could test a REST API service on which you depend.</span></span>

<span data-ttu-id="b57ef-111">Существует два вида тестов доступности:</span><span class="sxs-lookup"><span data-stu-id="b57ef-111">There are two types of availability tests:</span></span>

* <span data-ttu-id="b57ef-112">[Тест проверки связи с URL-адресом](#create)– простой тест, который вы можете создать на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b57ef-112">[URL ping test](#create): a simple test that you can create in the Azure portal.</span></span>
* <span data-ttu-id="b57ef-113">[Многошаговый веб-тест](#multi-step-web-tests) — тест, который вы создаете в Visual Studio Enterprise и загружаете на портал.</span><span class="sxs-lookup"><span data-stu-id="b57ef-113">[Multi-step web test](#multi-step-web-tests): which you create in Visual Studio Enterprise and upload to the portal.</span></span>

<span data-ttu-id="b57ef-114">Для одного ресурса приложения можно создать не более 25 тестов доступности.</span><span class="sxs-lookup"><span data-stu-id="b57ef-114">You can create up to 25 availability tests per application resource.</span></span>

## <span data-ttu-id="b57ef-115"><a name="create"></a>1. Открытие ресурса для отчетов по тестам доступности</span><span class="sxs-lookup"><span data-stu-id="b57ef-115"><a name="create"></a>1. Open a resource for your availability test reports</span></span>

<span data-ttu-id="b57ef-116">**Если вы уже настроили Application Insights** для веб-приложения, откройте ресурс Application Insights на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b57ef-116">**If you have already configured Application Insights** for your web app, open its Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="b57ef-117">**Чтобы увидеть отчеты в новом ресурсе**, зарегистрируйтесь в [Microsoft Azure](http://azure.com), перейдите на [портал Azure](https://portal.azure.com) и создайте ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b57ef-117">**Or, if you want to see your reports in a new resource,** sign up to [Microsoft Azure](http://azure.com), go to the [Azure portal](https://portal.azure.com), and create an Application Insights resource.</span></span>

![Создать > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

<span data-ttu-id="b57ef-119">Щелкните **Все ресурсы** , чтобы открыть колонку обзора для нового ресурса.</span><span class="sxs-lookup"><span data-stu-id="b57ef-119">Click **All resources** to open the Overview blade for the new resource.</span></span>

## <span data-ttu-id="b57ef-120"><a name="setup"></a>2. Создание теста проверки связи с URL-адресом</span><span class="sxs-lookup"><span data-stu-id="b57ef-120"><a name="setup"></a>2. Create a URL ping test</span></span>
<span data-ttu-id="b57ef-121">Откройте колонку "Доступность" и добавьте тест.</span><span class="sxs-lookup"><span data-stu-id="b57ef-121">Open the Availability blade and add a test.</span></span>

![Укажите хотя бы URL-адрес своего веб-сайта](./media/app-insights-monitor-web-app-availability/13-availability.png)

* <span data-ttu-id="b57ef-123">Вы можете указать **URL-адрес** любой веб-страницы, которую требуется протестировать, но он должен быть видимым из общедоступного Интернета.</span><span class="sxs-lookup"><span data-stu-id="b57ef-123">**The URL** can be any web page you want to test, but it must be visible from the public internet.</span></span> <span data-ttu-id="b57ef-124">URL-адрес может содержать строку запроса,</span><span class="sxs-lookup"><span data-stu-id="b57ef-124">The URL can include a query string.</span></span> <span data-ttu-id="b57ef-125">поэтому вы, например, сможете немного поупражняться в работе с базой данных.</span><span class="sxs-lookup"><span data-stu-id="b57ef-125">So, for example, you can exercise your database a little.</span></span> <span data-ttu-id="b57ef-126">Если URL-адрес указывает на перенаправление, мы будем переходить по нему до 10 раз.</span><span class="sxs-lookup"><span data-stu-id="b57ef-126">If the URL resolves to a redirect, we follow it up to 10 redirects.</span></span>
* <span data-ttu-id="b57ef-127">**Анализировать зависимые запросы.** Если этот флажок установлен, изображения, сценарии, файлы стилей и другие файлы, являющиеся частью тестируемых веб-страниц, запрашиваются для теста.</span><span class="sxs-lookup"><span data-stu-id="b57ef-127">**Parse dependent requests**: If this option is checked, the test requests images, scripts, style files, and other files that are part of the web page under test.</span></span> <span data-ttu-id="b57ef-128">Записанное время ответа включает время, затраченное на получение этих файлов.</span><span class="sxs-lookup"><span data-stu-id="b57ef-128">The recorded response time includes the time taken to get these files.</span></span> <span data-ttu-id="b57ef-129">Тест завершается ошибкой, если эти ресурсы не удается загрузить в течение времени ожидания, актуального для всего теста.</span><span class="sxs-lookup"><span data-stu-id="b57ef-129">The test fails if all these resources cannot be successfully downloaded within the timeout for the whole test.</span></span> 

    <span data-ttu-id="b57ef-130">Если этот флажок не установлен, то тест запросит только файл по указанному URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="b57ef-130">If the option is not checked, the test only requests the file at the URL you specified.</span></span>
* <span data-ttu-id="b57ef-131">**Enable retries** (Разрешить повторные попытки). Если этот флажок установлен, то при неудачном завершении тест будет повторяться через короткие интервалы.</span><span class="sxs-lookup"><span data-stu-id="b57ef-131">**Enable retries**:  If this option is checked, when the test fails, it is retried after a short interval.</span></span> <span data-ttu-id="b57ef-132">Сообщение об ошибке отобразится только после трех неудачных попыток подряд.</span><span class="sxs-lookup"><span data-stu-id="b57ef-132">A failure is reported only if three successive attempts fail.</span></span> <span data-ttu-id="b57ef-133">Последующие тесты будут выполняться с обычной частотой.</span><span class="sxs-lookup"><span data-stu-id="b57ef-133">Subsequent tests are then performed at the usual test frequency.</span></span> <span data-ttu-id="b57ef-134">Повторные попытки будут временно приостановлены до следующей успешной попытки.</span><span class="sxs-lookup"><span data-stu-id="b57ef-134">Retry is temporarily suspended until the next success.</span></span> <span data-ttu-id="b57ef-135">Это правило действует в любом расположении тестирования.</span><span class="sxs-lookup"><span data-stu-id="b57ef-135">This rule is applied independently at each test location.</span></span> <span data-ttu-id="b57ef-136">Этот вариант является рекомендуемым.</span><span class="sxs-lookup"><span data-stu-id="b57ef-136">We recommend this option.</span></span> <span data-ttu-id="b57ef-137">В среднем около 80 % неудачных попыток решаются при повторной попытке.</span><span class="sxs-lookup"><span data-stu-id="b57ef-137">On average, about 80% of failures disappear on retry.</span></span>
* <span data-ttu-id="b57ef-138">**Частота тестирования**: задает частоту выполнения теста из каждого тестового расположения.</span><span class="sxs-lookup"><span data-stu-id="b57ef-138">**Test frequency**: Sets how often the test is run from each test location.</span></span> <span data-ttu-id="b57ef-139">При частоте пять минут и с пятью тестовыми расположениями ваш сайт будет проверяться в среднем каждую минуту.</span><span class="sxs-lookup"><span data-stu-id="b57ef-139">With a frequency of five minutes and five test locations, your site is tested on average every minute.</span></span>
* <span data-ttu-id="b57ef-140">**Расположения тестирования** – это места, из которых наши серверы отправляют веб-запросы на ваш URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b57ef-140">**Test locations** are the places from where our servers send web requests to your URL.</span></span> <span data-ttu-id="b57ef-141">Выберите несколько расположений, чтобы можно было различать проблемы веб-сайта и сетевые проблемы.</span><span class="sxs-lookup"><span data-stu-id="b57ef-141">Choose more than one so that you can distinguish problems in your website from network issues.</span></span> <span data-ttu-id="b57ef-142">Вы можете выбрать до 16 таких расположений.</span><span class="sxs-lookup"><span data-stu-id="b57ef-142">You can select up to 16 locations.</span></span>
* <span data-ttu-id="b57ef-143">**Критерии успешного завершения**:</span><span class="sxs-lookup"><span data-stu-id="b57ef-143">**Success criteria**:</span></span>

    <span data-ttu-id="b57ef-144">**Время ожидания теста**: уменьшите значение этого параметра, чтобы получать оповещения о медленных откликах.</span><span class="sxs-lookup"><span data-stu-id="b57ef-144">**Test timeout**: Decrease this value to be alerted about slow responses.</span></span> <span data-ttu-id="b57ef-145">Тест считается неудачной попыткой, если ответы от сайта не были получены в течение заданного периода.</span><span class="sxs-lookup"><span data-stu-id="b57ef-145">The test is counted as a failure if the responses from your site have not been received within this period.</span></span> <span data-ttu-id="b57ef-146">Если выбрать параметр **Анализировать зависимые запросы**, все изображения, файлы стилей, скрипты и другие зависимые ресурсы будут получены в течение этого периода.</span><span class="sxs-lookup"><span data-stu-id="b57ef-146">If you selected **Parse dependent requests**, then all the images, style files, scripts, and other dependent resources must have been received within this period.</span></span>

    <span data-ttu-id="b57ef-147">**HTTP-ответ**: возвращаемый код состояния, который считается успешным результатом.</span><span class="sxs-lookup"><span data-stu-id="b57ef-147">**HTTP response**: The returned status code that is counted as a success.</span></span> <span data-ttu-id="b57ef-148">Код 200 указывает на возврат нормальной веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="b57ef-148">200 is the code that indicates that a normal web page has been returned.</span></span>

    <span data-ttu-id="b57ef-149">**Совпадение содержимого**: строка, например «Добро пожаловать!».</span><span class="sxs-lookup"><span data-stu-id="b57ef-149">**Content match**: a string, like "Welcome!"</span></span> <span data-ttu-id="b57ef-150">Проверим наличие точного совпадения (с учетом регистра) в каждом ответе.</span><span class="sxs-lookup"><span data-stu-id="b57ef-150">We test that an exact case-sensitive match occurs in every response.</span></span> <span data-ttu-id="b57ef-151">Это должна быть строка обычного текста без подстановочных знаков.</span><span class="sxs-lookup"><span data-stu-id="b57ef-151">It must be a plain string, without wildcards.</span></span> <span data-ttu-id="b57ef-152">Не забывайте, что если контент страницы изменяется, необходимо обновить эту строку.</span><span class="sxs-lookup"><span data-stu-id="b57ef-152">Don't forget that if your page content changes you might have to update it.</span></span>
* <span data-ttu-id="b57ef-153">**Оповещения** по умолчанию отправляются в случае неудачных попыток в трех расположениях на протяжении 5 минут.</span><span class="sxs-lookup"><span data-stu-id="b57ef-153">**Alerts** are, by default, sent to you if there are failures in three locations over five minutes.</span></span> <span data-ttu-id="b57ef-154">Сбой в одном расположении, вероятно, будет вызван проблемой с сетью, а не с сайтом.</span><span class="sxs-lookup"><span data-stu-id="b57ef-154">A failure in one location is likely to be a network problem, and not a problem with your site.</span></span> <span data-ttu-id="b57ef-155">Но для настройки чувствительности это пороговое значение можно изменить; можно также изменить адресатов, которые получат сообщения по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="b57ef-155">But you can change the threshold to be more or less sensitive, and you can also change who the emails should be sent to.</span></span>

    <span data-ttu-id="b57ef-156">Можно настроить вызов [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md), активируемый оповещением.</span><span class="sxs-lookup"><span data-stu-id="b57ef-156">You can set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span> <span data-ttu-id="b57ef-157">(Обратите внимание, что в настоящее время параметры запроса не передаются как свойства.)</span><span class="sxs-lookup"><span data-stu-id="b57ef-157">(But note that, at present, query parameters are not passed through as Properties.)</span></span>

### <a name="test-more-urls"></a><span data-ttu-id="b57ef-158">Тестирование дополнительных URL-адресов</span><span class="sxs-lookup"><span data-stu-id="b57ef-158">Test more URLs</span></span>
<span data-ttu-id="b57ef-159">Добавьте дополнительные тесты.</span><span class="sxs-lookup"><span data-stu-id="b57ef-159">Add more tests.</span></span> <span data-ttu-id="b57ef-160">Например, в дополнение к тестированию домашней страницы можно также проверить, запущена ли база данных, путем тестирования URL-адреса поиска.</span><span class="sxs-lookup"><span data-stu-id="b57ef-160">For example, In addition to testing your home page, you can make sure your database is running by testing the URL for a search.</span></span>


## <span data-ttu-id="b57ef-161"><a name="monitor"></a>3. Просмотр результатов теста доступности</span><span class="sxs-lookup"><span data-stu-id="b57ef-161"><a name="monitor"></a>3. See your availability test results</span></span>

<span data-ttu-id="b57ef-162">Через несколько минут щелкните **Обновить**, чтобы просмотреть результаты теста.</span><span class="sxs-lookup"><span data-stu-id="b57ef-162">After a few minutes, click **Refresh** to see test results.</span></span> 

![Сводка по результатам в домашнем разделе](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

<span data-ttu-id="b57ef-164">На точечной диаграмме отобразятся примеры результатов теста со сведениями о этапах диагностического теста.</span><span class="sxs-lookup"><span data-stu-id="b57ef-164">The scatterplot shows samples of the test results that have diagnostic test-step detail in them.</span></span> <span data-ttu-id="b57ef-165">Обработчик тестов хранит сведения о диагностике тестов, которые завершились сбоем.</span><span class="sxs-lookup"><span data-stu-id="b57ef-165">The test engine stores diagnostic detail for tests that have failures.</span></span> <span data-ttu-id="b57ef-166">Диагностические сведения об успешно выполненных тестах хранятся для подмножества выполнений.</span><span class="sxs-lookup"><span data-stu-id="b57ef-166">For successful tests, diagnostic details are stored for a subset of the executions.</span></span> <span data-ttu-id="b57ef-167">Наведите указатель мыши на любые красные или зеленые точки, чтобы просмотреть метку времени теста, длительность теста, местоположение и его имя.</span><span class="sxs-lookup"><span data-stu-id="b57ef-167">Hover over any of the green/red dots to see the test timestamp, test duration, location, and test name.</span></span> <span data-ttu-id="b57ef-168">Щелкните любую точку на точечной диаграмме, чтобы просмотреть сведения о результатах теста.</span><span class="sxs-lookup"><span data-stu-id="b57ef-168">Click through any dot in the scatter plot to see the details of the test result.</span></span>  

<span data-ttu-id="b57ef-169">Выберите конкретный тест, расположение или сократите период времени, чтобы просмотреть дополнительные результаты для нужного периода времени.</span><span class="sxs-lookup"><span data-stu-id="b57ef-169">Select a particular test, location, or reduce the time period to see more results around the time period of interest.</span></span> <span data-ttu-id="b57ef-170">Используйте обозреватель поиска, чтобы просмотреть результаты всех тестов или воспользуйтесь запросами аналитики, чтобы запустить пользовательские отчеты для этих данных.</span><span class="sxs-lookup"><span data-stu-id="b57ef-170">Use Search Explorer to see results from all executions, or use Analytics queries to run custom reports on this data.</span></span>

<span data-ttu-id="b57ef-171">Помимо необработанных результатов в обозревателе метрик имеются две метрики доступности:</span><span class="sxs-lookup"><span data-stu-id="b57ef-171">In addition to the raw results, there are two Availability metrics in Metrics Explorer:</span></span> 

1. <span data-ttu-id="b57ef-172">Доступность. Количество успешно выполненных тестов (в процентах).</span><span class="sxs-lookup"><span data-stu-id="b57ef-172">Availability: Percentage of the tests that were successful, across all test executions.</span></span> 
2. <span data-ttu-id="b57ef-173">Продолжительность теста. Средняя длительность всех тестов.</span><span class="sxs-lookup"><span data-stu-id="b57ef-173">Test Duration: Average test duration across all test executions.</span></span>

<span data-ttu-id="b57ef-174">Вы можете применить фильтры по имени теста или расположению, чтобы проанализировать тенденции конкретного теста и/или местоположения.</span><span class="sxs-lookup"><span data-stu-id="b57ef-174">You can apply filters on the test name, location to analyze trends of a particular test and/or location.</span></span>

## <span data-ttu-id="b57ef-175"><a name="edit"></a> Изменение и проверка тестов</span><span class="sxs-lookup"><span data-stu-id="b57ef-175"><a name="edit"></a> Inspect and edit tests</span></span>

<span data-ttu-id="b57ef-176">На странице сводки щелкните конкретный тест.</span><span class="sxs-lookup"><span data-stu-id="b57ef-176">From the summary page, select a specific test.</span></span> <span data-ttu-id="b57ef-177">Здесь можно просмотреть определенные результаты, а также изменить или временно отключить тест.</span><span class="sxs-lookup"><span data-stu-id="b57ef-177">There, you can see its specific results, and edit or temporarily disable it.</span></span>

![Изменение или отключение веб-теста](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

<span data-ttu-id="b57ef-179">При обслуживании службы может потребоваться отключить тесты доступности или правила оповещения, связанные с ними.</span><span class="sxs-lookup"><span data-stu-id="b57ef-179">You might want to disable availability tests or the alert rules associated with them while you are performing maintenance on your service.</span></span> 

## <span data-ttu-id="b57ef-180"><a name="failures"></a>При возникновении сбоев</span><span class="sxs-lookup"><span data-stu-id="b57ef-180"><a name="failures"></a>If you see failures</span></span>
<span data-ttu-id="b57ef-181">Щелкните красную точку.</span><span class="sxs-lookup"><span data-stu-id="b57ef-181">Click a red dot.</span></span>

![Щелкните красную точку.](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


<span data-ttu-id="b57ef-183">С помощью результатов тестов доступности можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="b57ef-183">From an availability test result, you can:</span></span>

* <span data-ttu-id="b57ef-184">изучить ответ, полученный от сервера;</span><span class="sxs-lookup"><span data-stu-id="b57ef-184">Inspect the response received from your server.</span></span>
* <span data-ttu-id="b57ef-185">открыть данные телеметрии, отправленные приложением сервера при обработке экземпляра запроса, завершившейся сбоем;</span><span class="sxs-lookup"><span data-stu-id="b57ef-185">Open the telemetry sent by your server app while processing the failed request instance.</span></span>
* <span data-ttu-id="b57ef-186">добавить в журнал проблему или зарегистрировать рабочий элемент в Git или VSTS для отслеживания проблемы;</span><span class="sxs-lookup"><span data-stu-id="b57ef-186">Log an issue or work item in Git or VSTS to track the problem.</span></span> <span data-ttu-id="b57ef-187">ошибка будет содержать ссылку на это событие;</span><span class="sxs-lookup"><span data-stu-id="b57ef-187">The bug will contain a link to this event.</span></span>
* <span data-ttu-id="b57ef-188">открыть результат веб-теста в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b57ef-188">Open the web test result in Visual Studio.</span></span>


<span data-ttu-id="b57ef-189">*Кажется, что все работает правильно, но выдается отчет об ошибке?*</span><span class="sxs-lookup"><span data-stu-id="b57ef-189">*Looks OK but reported as a failure?*</span></span> <span data-ttu-id="b57ef-190">Проверьте все изображения, скрипты, таблицы стилей и любые другие файлы, загружаемые на страницу.</span><span class="sxs-lookup"><span data-stu-id="b57ef-190">Check all the images, scripts, style sheets, and any other files loaded by the page.</span></span> <span data-ttu-id="b57ef-191">Если не удается загрузить какой-либо компонент, отчет о тесте выдаст ошибку, даже если главная HTML-страница загружается правильно.</span><span class="sxs-lookup"><span data-stu-id="b57ef-191">If any of them fails, the test is reported as failed, even if the main html page loads OK.</span></span>

<span data-ttu-id="b57ef-192">*Связанные элементы отсутствуют?*</span><span class="sxs-lookup"><span data-stu-id="b57ef-192">*No related items?*</span></span> <span data-ttu-id="b57ef-193">Если служба Application Insights настроена для серверного приложения, возможно, это произошло из-за [выборки](app-insights-sampling.md) в операции.</span><span class="sxs-lookup"><span data-stu-id="b57ef-193">If you have Application Insights set up for your server-side application, that may be because [sampling](app-insights-sampling.md) is in operation.</span></span> 

## <a name="multi-step-web-tests"></a><span data-ttu-id="b57ef-194">Многошаговые веб-тесты</span><span class="sxs-lookup"><span data-stu-id="b57ef-194">Multi-step web tests</span></span>
<span data-ttu-id="b57ef-195">Вы можете отслеживать сценарий, который содержит последовательность URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="b57ef-195">You can monitor a scenario that involves a sequence of URLs.</span></span> <span data-ttu-id="b57ef-196">Например, в случае наблюдения за интернет-магазином вы можете проверить, что добавление товаров в корзину работает исправно.</span><span class="sxs-lookup"><span data-stu-id="b57ef-196">For example, if you are monitoring a sales website, you can test that adding items to the shopping cart works correctly.</span></span>

> [!NOTE] 
> <span data-ttu-id="b57ef-197">За многошаговые веб-тесты взимается плата.</span><span class="sxs-lookup"><span data-stu-id="b57ef-197">There is a charge for multi-step web tests.</span></span> <span data-ttu-id="b57ef-198">См. [таблицу расценок](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="b57ef-198">[Pricing scheme](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>
> 

<span data-ttu-id="b57ef-199">Для создания многошагового теста вам сначала нужно записать сценарий с помощью Visual Studio Enterprise, а затем отправить запись в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b57ef-199">To create a multi-step test, you record the scenario by using Visual Studio Enterprise, and then upload the recording to Application Insights.</span></span> <span data-ttu-id="b57ef-200">Application Insights периодически воспроизводит сценарий и проверяет ответы.</span><span class="sxs-lookup"><span data-stu-id="b57ef-200">Application Insights replays the scenario at intervals and verifies the responses.</span></span>

> [!NOTE]
> <span data-ttu-id="b57ef-201">В тестах нельзя использовать запрограммированные функции или циклы.</span><span class="sxs-lookup"><span data-stu-id="b57ef-201">You can't use coded functions or loops in your tests.</span></span> <span data-ttu-id="b57ef-202">Тест должен полностью находиться в WEBTEST-файле скрипта.</span><span class="sxs-lookup"><span data-stu-id="b57ef-202">The test must be contained completely in the .webtest script.</span></span> <span data-ttu-id="b57ef-203">Однако вы можете использовать стандартные подключаемые модули.</span><span class="sxs-lookup"><span data-stu-id="b57ef-203">However, you can use standard plugins.</span></span>
>

#### <a name="1-record-a-scenario"></a><span data-ttu-id="b57ef-204">1. Запись сценария</span><span class="sxs-lookup"><span data-stu-id="b57ef-204">1. Record a scenario</span></span>
<span data-ttu-id="b57ef-205">Для записи веб-сеанса используйте Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b57ef-205">Use Visual Studio Enterprise to record a web session.</span></span>

1. <span data-ttu-id="b57ef-206">Создайте проект веб-теста производительности.</span><span class="sxs-lookup"><span data-stu-id="b57ef-206">Create a Web performance test project.</span></span>

    ![В Visual Studio Enterprise создайте новый проект на основе шаблона с веб-тестами производительности и нагрузочными тестами.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * <span data-ttu-id="b57ef-208">*Отсутствует шаблон с веб-тестами производительности и нагрузочными тестами?*</span><span class="sxs-lookup"><span data-stu-id="b57ef-208">*Don't see the Web Performance and Load Test template?*</span></span> <span data-ttu-id="b57ef-209">Закройте Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b57ef-209">- Close Visual Studio Enterprise.</span></span> <span data-ttu-id="b57ef-210">Откройте **установщик Visual Studio**, чтобы изменить установленные компоненты Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b57ef-210">Open **Visual Studio Installer** to modify your Visual Studio Enterprise installation.</span></span> <span data-ttu-id="b57ef-211">В разделе **Отдельные компоненты** выберите **Средства для тестирования производительности веб-сайтов и нагрузочного тестирования**.</span><span class="sxs-lookup"><span data-stu-id="b57ef-211">Under **Individual Components**, select **Web Performance and load testing tools**.</span></span>

2. <span data-ttu-id="b57ef-212">Откройте WEBTEST-файл и начните запись.</span><span class="sxs-lookup"><span data-stu-id="b57ef-212">Open the .webtest file and start recording.</span></span>

    ![Откройте WEBTEST-файл и щелкните "Запись".](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. <span data-ttu-id="b57ef-214">Выполните действия пользователя, которые нужно смоделировать в тесте: откройте веб-сайт, добавьте продукт в корзину и т. д.</span><span class="sxs-lookup"><span data-stu-id="b57ef-214">Do the user actions you want to simulate in your test: open your website, add a product to the cart, and so on.</span></span> <span data-ttu-id="b57ef-215">Затем остановите тест.</span><span class="sxs-lookup"><span data-stu-id="b57ef-215">Then stop your test.</span></span>

    ![Запись веб-теста выполняется в Internet Explorer.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    <span data-ttu-id="b57ef-217">Не делайте слишком длинный сценарий.</span><span class="sxs-lookup"><span data-stu-id="b57ef-217">Don't make a long scenario.</span></span> <span data-ttu-id="b57ef-218">Ограничение — 100 шагов и 2 минуты.</span><span class="sxs-lookup"><span data-stu-id="b57ef-218">There's a limit of 100 steps and 2 minutes.</span></span>
4. <span data-ttu-id="b57ef-219">Отредактируйте тест, чтобы:</span><span class="sxs-lookup"><span data-stu-id="b57ef-219">Edit the test to:</span></span>

   * <span data-ttu-id="b57ef-220">Добавить проверки полученного текста и кодов ответов.</span><span class="sxs-lookup"><span data-stu-id="b57ef-220">Add validations to check the received text and response codes.</span></span>
   * <span data-ttu-id="b57ef-221">Удалить все лишние взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="b57ef-221">Remove any superfluous interactions.</span></span> <span data-ttu-id="b57ef-222">Вы также можете удалить связанные запросы изображений, запросы к рекламным сайтам или сайтам отслеживания.</span><span class="sxs-lookup"><span data-stu-id="b57ef-222">You could also remove dependent requests for pictures or to ad or tracking sites.</span></span>

     <span data-ttu-id="b57ef-223">Помните, что редактировать можно только тестовый сценарий — добавлять собственный код и вызывать другие веб-тесты нельзя.</span><span class="sxs-lookup"><span data-stu-id="b57ef-223">Remember that you can only edit the test script - you can't add custom code or call other web tests.</span></span> <span data-ttu-id="b57ef-224">Не вставляйте в тест циклы.</span><span class="sxs-lookup"><span data-stu-id="b57ef-224">Don't insert loops in the test.</span></span> <span data-ttu-id="b57ef-225">Вы можете использовать стандартные подключаемые модули для веб-тестов.</span><span class="sxs-lookup"><span data-stu-id="b57ef-225">You can use standard web test plug-ins.</span></span>
5. <span data-ttu-id="b57ef-226">Запустите тест в Visual Studio и убедитесь, что он работает.</span><span class="sxs-lookup"><span data-stu-id="b57ef-226">Run the test in Visual Studio to make sure it works.</span></span>

    <span data-ttu-id="b57ef-227">Средство выполнения веб-тестов откроет веб-браузер и повторит записанные действия.</span><span class="sxs-lookup"><span data-stu-id="b57ef-227">The web test runner opens a web browser and repeats the actions you recorded.</span></span> <span data-ttu-id="b57ef-228">Убедитесь, что тест работает правильно.</span><span class="sxs-lookup"><span data-stu-id="b57ef-228">Make sure it works as you expect.</span></span>

    ![В Visual Studio откройте WEBTEST-файл и щелкните "Выполнить".](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-the-web-test-to-application-insights"></a><span data-ttu-id="b57ef-230">2) Загрузка веб-теста в Application Insights</span><span class="sxs-lookup"><span data-stu-id="b57ef-230">2. Upload the web test to Application Insights</span></span>
1. <span data-ttu-id="b57ef-231">Создайте веб-тест на портале Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b57ef-231">In the Application Insights portal, create a web test.</span></span>

    ![В колонке "Веб-тесты" нажмите кнопку "Добавить".](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. <span data-ttu-id="b57ef-233">Выберите многошаговый тест и загрузите WEBTEST-файл.</span><span class="sxs-lookup"><span data-stu-id="b57ef-233">Select multi-step test, and upload the .webtest file.</span></span>

    ![Выберите многошаговый веб-тест.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    <span data-ttu-id="b57ef-235">Установите для тестовых местоположений, частоты и параметров оповещения те же значения, что и для проверок связи.</span><span class="sxs-lookup"><span data-stu-id="b57ef-235">Set the test locations, frequency, and alert parameters in the same way as for ping tests.</span></span>

#### <a name="3-see-the-results"></a><span data-ttu-id="b57ef-236">3. Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="b57ef-236">3. See the results</span></span>

<span data-ttu-id="b57ef-237">Просмотр результатов теста и всех ошибок выполняется так же, как и для тестов с одним URL.</span><span class="sxs-lookup"><span data-stu-id="b57ef-237">View your test results and any failures in the same way as single-url tests.</span></span>

<span data-ttu-id="b57ef-238">Кроме того, можно скачать результаты теста, чтобы просмотреть их в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b57ef-238">In addition, you can download the test results to view them in Visual Studio.</span></span>

#### <a name="too-many-failures"></a><span data-ttu-id="b57ef-239">Слишком много ошибок?</span><span class="sxs-lookup"><span data-stu-id="b57ef-239">Too many failures?</span></span>

* <span data-ttu-id="b57ef-240">Распространенной причиной ошибок является слишком большое время выполнения теста.</span><span class="sxs-lookup"><span data-stu-id="b57ef-240">A common reason for failure is that the test runs too long.</span></span> <span data-ttu-id="b57ef-241">Тест должен выполняться не более двух минут.</span><span class="sxs-lookup"><span data-stu-id="b57ef-241">It mustn't run longer than two minutes.</span></span>

* <span data-ttu-id="b57ef-242">Помните, что для успешного завершения теста на страницу должны корректно загрузиться все ресурсы, в том числе сценарии, таблицы стилей, изображения и т. д.</span><span class="sxs-lookup"><span data-stu-id="b57ef-242">Don't forget that all the resources of a page must load correctly for the test to succeed, including scripts, style sheets, images, and so forth.</span></span>

* <span data-ttu-id="b57ef-243">Веб-тест должен полностью содержаться в WEBTEST-файле скрипта: в тесте нельзя использовать запрограммированные функции.</span><span class="sxs-lookup"><span data-stu-id="b57ef-243">The web test must be entirely contained in the .webtest script: you can't use coded functions in the test.</span></span>

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a><span data-ttu-id="b57ef-244">Вставка времени и случайных чисел в многошаговый тест</span><span class="sxs-lookup"><span data-stu-id="b57ef-244">Plugging time and random numbers into your multi-step test</span></span>
<span data-ttu-id="b57ef-245">Предположим, что вы тестируете инструмент, который получает зависящие от времени данные (например, запасы) от внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="b57ef-245">Suppose you're testing a tool that gets time-dependent data such as stocks from an external feed.</span></span> <span data-ttu-id="b57ef-246">При записи веб-теста необходимо использовать определенные значения времени, но они должны быть заданы как параметры теста StartTime и EndTime.</span><span class="sxs-lookup"><span data-stu-id="b57ef-246">When you record your web test, you have to use specific times, but you set them as parameters of the test, StartTime and EndTime.</span></span>

![Веб-тест с параметрами.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

<span data-ttu-id="b57ef-248">При запуске теста параметру EndTime следует всегда присваивать текущее время, а параметру StartTime – время за 15 минут до текущего.</span><span class="sxs-lookup"><span data-stu-id="b57ef-248">When you run the test, you'd like EndTime always to be the present time, and StartTime should be 15 minutes ago.</span></span>

<span data-ttu-id="b57ef-249">Подключаемые модули веб-теста позволяют параметризовать время.</span><span class="sxs-lookup"><span data-stu-id="b57ef-249">Web Test Plug-ins provide the way to do parameterize times.</span></span>

1. <span data-ttu-id="b57ef-250">Добавьте подключаемые модули веб-теста для всех необходимых значений переменных параметров.</span><span class="sxs-lookup"><span data-stu-id="b57ef-250">Add a web test plug-in for each variable parameter value you want.</span></span> <span data-ttu-id="b57ef-251">На панели инструментов веб-теста выберите **Добавить подключаемый модуль веб-теста**.</span><span class="sxs-lookup"><span data-stu-id="b57ef-251">In the web test toolbar, choose **Add Web Test Plugin**.</span></span>

    ![Щелкните "Добавить подключаемый модуль веб-теста" и выберите тип.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    <span data-ttu-id="b57ef-253">В этом примере используется два экземпляра подключаемого модуля даты и времени.</span><span class="sxs-lookup"><span data-stu-id="b57ef-253">In this example, we use two instances of the Date Time Plug-in.</span></span> <span data-ttu-id="b57ef-254">Для первого экземпляра будет задано время за 15 минут до текущего, а для второго — текущее время.</span><span class="sxs-lookup"><span data-stu-id="b57ef-254">One instance is for "15 minutes ago" and another for "now."</span></span>
2. <span data-ttu-id="b57ef-255">Откройте свойства каждого подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="b57ef-255">Open the properties of each plug-in.</span></span> <span data-ttu-id="b57ef-256">Присвойте ему имя и настройте его для использования текущего времени.</span><span class="sxs-lookup"><span data-stu-id="b57ef-256">Give it a name and set it to use the current time.</span></span> <span data-ttu-id="b57ef-257">Для одного из экземпляров задайте для параметра "Добавление минут" значение "-15".</span><span class="sxs-lookup"><span data-stu-id="b57ef-257">For one of them, set Add Minutes = -15.</span></span>

    ![Задайте имя, выберите "Использовать текущее время" и "Добавить минуты".](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. <span data-ttu-id="b57ef-259">В параметрах веб-теста используйте {{имя подключаемого модуля}} для ссылки на имя подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="b57ef-259">In the web test parameters, use {{plug-in name}} to reference a plug-in name.</span></span>

    ![В параметрах теста используйте {{имя подключаемого модуля}}.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

<span data-ttu-id="b57ef-261">Теперь можно передать тест на портал.</span><span class="sxs-lookup"><span data-stu-id="b57ef-261">Now, upload your test to the portal.</span></span> <span data-ttu-id="b57ef-262">Он использует динамические значения при каждом тестировании.</span><span class="sxs-lookup"><span data-stu-id="b57ef-262">It uses the dynamic values on every run of the test.</span></span>

## <a name="dealing-with-sign-in"></a><span data-ttu-id="b57ef-263">Работа с входом</span><span class="sxs-lookup"><span data-stu-id="b57ef-263">Dealing with sign-in</span></span>
<span data-ttu-id="b57ef-264">Если пользователи входят в приложение, вы можете протестировать страницы входа, используя несколько способов имитации входа.</span><span class="sxs-lookup"><span data-stu-id="b57ef-264">If your users sign in to your app, you have various options for simulating sign-in so that you can test pages behind the sign-in.</span></span> <span data-ttu-id="b57ef-265">Выбор подхода зависит от типа безопасности в приложении.</span><span class="sxs-lookup"><span data-stu-id="b57ef-265">The approach you use depends on the type of security provided by the app.</span></span>

<span data-ttu-id="b57ef-266">Во всех случаях учетную запись в приложении следует создавать только для целей тестирования.</span><span class="sxs-lookup"><span data-stu-id="b57ef-266">In all cases, you should create an account in your application just for the purpose of testing.</span></span> <span data-ttu-id="b57ef-267">По возможности ограничьте разрешения для этой тестовой учетной записи, чтобы веб-тесты не доставляли неудобств реальным пользователям.</span><span class="sxs-lookup"><span data-stu-id="b57ef-267">If possible, restrict the permissions of this test account so that there's no possibility of the web tests affecting real users.</span></span>

### <a name="simple-username-and-password"></a><span data-ttu-id="b57ef-268">Простое имя пользователя и пароль</span><span class="sxs-lookup"><span data-stu-id="b57ef-268">Simple username and password</span></span>
<span data-ttu-id="b57ef-269">Запишите веб-тест обычным образом.</span><span class="sxs-lookup"><span data-stu-id="b57ef-269">Record a web test in the usual way.</span></span> <span data-ttu-id="b57ef-270">Сначала удалите файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="b57ef-270">Delete cookies first.</span></span>

### <a name="saml-authentication"></a><span data-ttu-id="b57ef-271">Проверка подлинности SAML</span><span class="sxs-lookup"><span data-stu-id="b57ef-271">SAML authentication</span></span>
<span data-ttu-id="b57ef-272">Используйте подключаемый модуль SAML, доступный для веб-тестов.</span><span class="sxs-lookup"><span data-stu-id="b57ef-272">Use the SAML plugin that is available for web tests.</span></span>

### <a name="client-secret"></a><span data-ttu-id="b57ef-273">Секрет клиента</span><span class="sxs-lookup"><span data-stu-id="b57ef-273">Client secret</span></span>
<span data-ttu-id="b57ef-274">Если в приложении предусмотрен маршрут входа с использованием секрета клиента, используйте этот маршрут.</span><span class="sxs-lookup"><span data-stu-id="b57ef-274">If your app has a sign-in route that involves a client secret, use that route.</span></span> <span data-ttu-id="b57ef-275">Azure Active Directory (AAD) — это пример службы, в которой доступен вход в систему с использованием секрета клиента.</span><span class="sxs-lookup"><span data-stu-id="b57ef-275">Azure Active Directory (AAD) is an example of a service that provides a client secret sign-in.</span></span> <span data-ttu-id="b57ef-276">В AAD секрет клиента — это ключ приложения.</span><span class="sxs-lookup"><span data-stu-id="b57ef-276">In AAD, the client secret is the App Key.</span></span>

<span data-ttu-id="b57ef-277">Ниже приведен пример веб-теста веб-приложения Azure с использованием ключа приложения.</span><span class="sxs-lookup"><span data-stu-id="b57ef-277">Here's a sample web test of an Azure web app using an app key:</span></span>

![Пример секрета клиента](./media/app-insights-monitor-web-app-availability/110.png)

1. <span data-ttu-id="b57ef-279">Получите токен из Azure AD с помощью секрета клиента (AppKey).</span><span class="sxs-lookup"><span data-stu-id="b57ef-279">Get token from AAD using client secret (AppKey).</span></span>
2. <span data-ttu-id="b57ef-280">Извлеките токен носителя из ответа.</span><span class="sxs-lookup"><span data-stu-id="b57ef-280">Extract bearer token from response.</span></span>
3. <span data-ttu-id="b57ef-281">Вызовите интерфейс API, используя токен носителя в заголовке авторизации.</span><span class="sxs-lookup"><span data-stu-id="b57ef-281">Call API using bearer token in the authorization header.</span></span>

<span data-ttu-id="b57ef-282">Убедитесь, что веб-тест является фактическим клиентом, т. е. у него есть собственное приложение в AAD, и используйте его значения clientId и appkey.</span><span class="sxs-lookup"><span data-stu-id="b57ef-282">Make sure that the web test is an actual client - that is, it has its own app in AAD - and use its clientId + appkey.</span></span> <span data-ttu-id="b57ef-283">У тестируемой службы также есть собственное приложение в AAD: универсальный код ресурса URI appID этого приложения содержится в веб-тесте в поле resource.</span><span class="sxs-lookup"><span data-stu-id="b57ef-283">Your service under test also has its own app in AAD: the appID URI of this app is reflected in the web test in the “resource” field.</span></span>

### <a name="open-authentication"></a><span data-ttu-id="b57ef-284">Открытая проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="b57ef-284">Open Authentication</span></span>
<span data-ttu-id="b57ef-285">Пример открытой проверки подлинности — это вход с помощью учетной записи Майкрософт или Google.</span><span class="sxs-lookup"><span data-stu-id="b57ef-285">An example of open authentication is signing in with your Microsoft or Google account.</span></span> <span data-ttu-id="b57ef-286">Многие приложения, использующие OAuth, предоставляют альтернативный вариант с использованием секрета клиента, поэтому сначала стоит попробовать эту возможность.</span><span class="sxs-lookup"><span data-stu-id="b57ef-286">Many apps that use OAuth provide the client secret alternative, so your first tactic should be to investigate that possibility.</span></span>

<span data-ttu-id="b57ef-287">Если в вашем тесте должен выполняться вход с использованием OAuth, общий порядок действий таков:</span><span class="sxs-lookup"><span data-stu-id="b57ef-287">If your test must sign in using OAuth, the general approach is:</span></span>

* <span data-ttu-id="b57ef-288">Проверьте трафик между веб-браузером, сайтом проверки подлинности и приложением при помощи Fiddler или аналогичного средства.</span><span class="sxs-lookup"><span data-stu-id="b57ef-288">Use a tool such as Fiddler to examine the traffic between your web browser, the authentication site, and your app.</span></span>
* <span data-ttu-id="b57ef-289">Выполните вход несколько раз с разных компьютеров или из разных браузеров либо через большие промежутки времени (чтобы истек срок действия маркеров).</span><span class="sxs-lookup"><span data-stu-id="b57ef-289">Perform two or more sign-ins using different machines or browsers, or at long intervals (to allow tokens to expire).</span></span>
* <span data-ttu-id="b57ef-290">Сравнивая различные сеансы, определите маркер, возвращаемый с сайта проверки подлинности, который затем передается на сервер приложения после входа.</span><span class="sxs-lookup"><span data-stu-id="b57ef-290">By comparing different sessions, identify the token passed back from the authenticating site, that is then passed to your app server after sign-in.</span></span>
* <span data-ttu-id="b57ef-291">Запишите веб-тест с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b57ef-291">Record a web test using Visual Studio.</span></span>
* <span data-ttu-id="b57ef-292">Параметризуйте маркеры, задав параметр при возврате маркера из структуры проверки подлинности и использовав его в запросе к сайту.</span><span class="sxs-lookup"><span data-stu-id="b57ef-292">Parameterize the tokens, setting the parameter when the token is returned from the authenticator, and using it in the query to the site.</span></span>
  <span data-ttu-id="b57ef-293">(Visual Studio попытается параметризовать тест, но не сможет правильно параметризовать маркеры).</span><span class="sxs-lookup"><span data-stu-id="b57ef-293">(Visual Studio attempts to parameterize the test, but does not correctly parameterize the tokens.)</span></span>


## <a name="performance-tests"></a><span data-ttu-id="b57ef-294">Тесты производительности</span><span class="sxs-lookup"><span data-stu-id="b57ef-294">Performance tests</span></span>
<span data-ttu-id="b57ef-295">Вы можете выполнить на своем веб-сайте нагрузочный тест.</span><span class="sxs-lookup"><span data-stu-id="b57ef-295">You can run a load test on your website.</span></span> <span data-ttu-id="b57ef-296">Как и при проверке доступности, вы можете отправлять простые или многошаговые запросы из точек по всему миру.</span><span class="sxs-lookup"><span data-stu-id="b57ef-296">Like the availability test, you can send either simple requests or multi-step requests from our points around the world.</span></span> <span data-ttu-id="b57ef-297">В отличие от теста доступности, отправляется много запросов, что имитирует несколько одновременно работающих пользователей.</span><span class="sxs-lookup"><span data-stu-id="b57ef-297">Unlike an availability test, many requests are sent, simulating multiple simultaneous users.</span></span>

<span data-ttu-id="b57ef-298">В колонке "Обзор" выберите **Параметры** и **Тесты производительности**.</span><span class="sxs-lookup"><span data-stu-id="b57ef-298">From the Overview blade, open **Settings**, **Performance Tests**.</span></span> <span data-ttu-id="b57ef-299">При создании теста вам будет предложено подключиться к учетной записи служб Visual Studio Team Services или создать ее.</span><span class="sxs-lookup"><span data-stu-id="b57ef-299">When you create a test, you are invited to connect to or create a Visual Studio Team Services account.</span></span>

<span data-ttu-id="b57ef-300">По завершении теста на экране отобразится время ответа и число успешных попыток.</span><span class="sxs-lookup"><span data-stu-id="b57ef-300">When the test is complete, you are shown response times and success rates.</span></span>


![тест производительности;](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> <span data-ttu-id="b57ef-302">Чтобы увидеть результаты теста производительности, используйте [Live Stream](app-insights-live-stream.md) и [профилировщик](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="b57ef-302">To observe the effects of a performance test, use [Live Stream](app-insights-live-stream.md) and [Profiler](app-insights-profiler.md).</span></span>
>

## <a name="automation"></a><span data-ttu-id="b57ef-303">Автоматизация</span><span class="sxs-lookup"><span data-stu-id="b57ef-303">Automation</span></span>
* <span data-ttu-id="b57ef-304">[Используйте сценарии PowerShell, чтобы настройка теста доступности](app-insights-powershell.md#add-an-availability-test) выполнялась автоматически.</span><span class="sxs-lookup"><span data-stu-id="b57ef-304">[Use PowerShell scripts to set up an availability test](app-insights-powershell.md#add-an-availability-test) automatically.</span></span>
* <span data-ttu-id="b57ef-305">Настройте вызов [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md), активируемый оповещением.</span><span class="sxs-lookup"><span data-stu-id="b57ef-305">Set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span>

## <span data-ttu-id="b57ef-306"><a name="qna"></a>Вопросы?</span><span class="sxs-lookup"><span data-stu-id="b57ef-306"><a name="qna"></a>Questions?</span></span> <span data-ttu-id="b57ef-307">Проблемы?</span><span class="sxs-lookup"><span data-stu-id="b57ef-307">Problems?</span></span>
* <span data-ttu-id="b57ef-308">*Можно ли вызывать код из моего веб-теста?*</span><span class="sxs-lookup"><span data-stu-id="b57ef-308">*Can I call code from my web test?*</span></span>

    <span data-ttu-id="b57ef-309">Нет.</span><span class="sxs-lookup"><span data-stu-id="b57ef-309">No.</span></span> <span data-ttu-id="b57ef-310">Действия теста должны находиться в WEBTEST-файле.</span><span class="sxs-lookup"><span data-stu-id="b57ef-310">The steps of the test must be in the .webtest file.</span></span> <span data-ttu-id="b57ef-311">Кроме того, нельзя вызывать другие веб-тесты и использовать циклы.</span><span class="sxs-lookup"><span data-stu-id="b57ef-311">And you can't call other web tests or use loops.</span></span> <span data-ttu-id="b57ef-312">Но есть несколько подключаемых модулей, которые могут оказаться полезными.</span><span class="sxs-lookup"><span data-stu-id="b57ef-312">But there are several plug-ins that you might find helpful.</span></span>
* <span data-ttu-id="b57ef-313">*Поддерживается ли протокол HTTPS?*</span><span class="sxs-lookup"><span data-stu-id="b57ef-313">*Is HTTPS supported?*</span></span>

    <span data-ttu-id="b57ef-314">Мы поддерживаем TLS 1.1 и TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="b57ef-314">We support TLS 1.1 and TLS 1.2.</span></span>
* <span data-ttu-id="b57ef-315">*Есть ли разница между понятиями «веб-тесты» и «тесты доступности»?*</span><span class="sxs-lookup"><span data-stu-id="b57ef-315">*Is there a difference between "web tests" and "availability tests"?*</span></span>

    <span data-ttu-id="b57ef-316">Эти два термина могут быть взаимозаменяемыми.</span><span class="sxs-lookup"><span data-stu-id="b57ef-316">The two terms may be referenced interchangeably.</span></span> <span data-ttu-id="b57ef-317">Тест доступности является более универсальным термином, так как кроме многошаговых веб-тестов вам доступны проверка связи с отдельным URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="b57ef-317">Availability tests is a more generic term that includes the single URL ping tests in addition to the multi-step web tests.</span></span>
* <span data-ttu-id="b57ef-318">*Мне нужно использовать тесты доступности на нашем внутреннем сервере, который работает за брандмауэром.*</span><span class="sxs-lookup"><span data-stu-id="b57ef-318">*I'd like to use availability tests on our internal server that runs behind a firewall.*</span></span>

    <span data-ttu-id="b57ef-319">Есть два возможных решения:</span><span class="sxs-lookup"><span data-stu-id="b57ef-319">There are two possible solutions:</span></span>
    
    * <span data-ttu-id="b57ef-320">Разрешите в брандмауэре входящие запросы с [IP-адресов агентов веб-тестирования](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="b57ef-320">Configure your firewall to permit incoming requests from the [IP addresses of our web test agents](app-insights-ip-addresses.md).</span></span>
    * <span data-ttu-id="b57ef-321">Напишите собственный код для периодической проверки внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b57ef-321">Write your own code to periodically test your internal server.</span></span> <span data-ttu-id="b57ef-322">Запустите код в виде фонового процесса на тестовом сервере за брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="b57ef-322">Run the code as a background process on a test server behind your firewall.</span></span> <span data-ttu-id="b57ef-323">Процесс тестирования может отправлять результаты в Application Insights с помощью API [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) в основном пакете SDK.</span><span class="sxs-lookup"><span data-stu-id="b57ef-323">Your test process can send its results to Application Insights by using [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API in the core SDK package.</span></span> <span data-ttu-id="b57ef-324">Для этого тестовый сервер должен иметь исходящий доступ к конечной точке приема в Application Insights, что представляет гораздо меньшую угрозу безопасности, чем разрешение входящих запросов.</span><span class="sxs-lookup"><span data-stu-id="b57ef-324">This requires your test server to have outgoing access to the Application Insights ingestion endpoint, but that is a much smaller security risk than the alternative of permitting incoming requests.</span></span> <span data-ttu-id="b57ef-325">Результаты не будут отображаться в колонках веб-тестов доступности, но будут отображаться как результаты в обозревателе метрик, поиска и анализа.</span><span class="sxs-lookup"><span data-stu-id="b57ef-325">The results will not appear in the availability web tests blades, but appears as availability results in Analytics, Search, and Metric Explorer.</span></span>
* <span data-ttu-id="b57ef-326">*Сбой отправки многошагового веб-теста.*</span><span class="sxs-lookup"><span data-stu-id="b57ef-326">*Uploading a multi-step web test fails*</span></span>

    <span data-ttu-id="b57ef-327">Максимальный размер — 300 000.</span><span class="sxs-lookup"><span data-stu-id="b57ef-327">There's a size limit of 300 K.</span></span>

    <span data-ttu-id="b57ef-328">Циклы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b57ef-328">Loops aren't supported.</span></span>

    <span data-ttu-id="b57ef-329">Ссылки на другие веб-тесты не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b57ef-329">References to other web tests aren't supported.</span></span>

    <span data-ttu-id="b57ef-330">Источники данных не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b57ef-330">Data sources aren't supported.</span></span>
* <span data-ttu-id="b57ef-331">*Мой многошаговый тест не выполняется.*</span><span class="sxs-lookup"><span data-stu-id="b57ef-331">*My multi-step test doesn't complete*</span></span>

    <span data-ttu-id="b57ef-332">Максимальное количество запросов в тесте — 100.</span><span class="sxs-lookup"><span data-stu-id="b57ef-332">There's a limit of 100 requests per test.</span></span>

    <span data-ttu-id="b57ef-333">Тест будет остановлен, если он выполняется дольше двух минут.</span><span class="sxs-lookup"><span data-stu-id="b57ef-333">The test is stopped if it runs longer than two minutes.</span></span>
* <span data-ttu-id="b57ef-334">*Как запустить тест с клиентскими сертификатами?*</span><span class="sxs-lookup"><span data-stu-id="b57ef-334">*How can I run a test with client certificates?*</span></span>

    <span data-ttu-id="b57ef-335">К сожалению, эта возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b57ef-335">We don't support that, sorry.</span></span>


## <span data-ttu-id="b57ef-336"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b57ef-336"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="b57ef-337">[Поиск по журналу диагностики в Application Insights][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="b57ef-337">[Search diagnostic logs][diagnostic]</span></span>

<span data-ttu-id="b57ef-338">[Устранение неполадок][qna]</span><span class="sxs-lookup"><span data-stu-id="b57ef-338">[Troubleshooting][qna]</span></span>

[<span data-ttu-id="b57ef-339">IP-адреса веб-агентов тестирования</span><span class="sxs-lookup"><span data-stu-id="b57ef-339">IP addresses of web test agents</span></span>](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
