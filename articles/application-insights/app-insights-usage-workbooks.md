---
title: "данные об использовании aaaInvestigate и общая папка с интерактивные книги в Azure Application Insights | Документы Microsoft"
description: "Демографический анализ пользователей веб-приложения."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="bec3d-103">Изучение и предоставление общего доступа к данным об использовании c интерактивными книгами в Application Insights</span><span class="sxs-lookup"><span data-stu-id="bec3d-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="bec3d-104">Workbooks объединяют визуализации данных [Azure Application Insights](app-insights-overview.md), [запросы аналитики](app-insights-analytics.md) и текст в интерактивных документах.</span><span class="sxs-lookup"><span data-stu-id="bec3d-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="bec3d-105">Книги можно редактировать другими членами группы с доступом toohello же ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="bec3d-105">Workbooks are editable by other team members with access toohello same Azure resource.</span></span> <span data-ttu-id="bec3d-106">Это означает, что hello элементов управления и запросов используется toocreate книги, доступных tooother посетителей hello книги, что делает их легко tooexplore, расширения и проверьте наличие ошибок.</span><span class="sxs-lookup"><span data-stu-id="bec3d-106">This means hello queries and controls used toocreate a workbook are available tooother people reading hello workbook, making them easy tooexplore, extend, and check for mistakes.</span></span>

<span data-ttu-id="bec3d-107">Workbooks полезны для следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="bec3d-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="bec3d-108">Изучение hello использование приложения, если вам не известно заранее метрики hello интерес: количество пользователей, коэффициент хранения, курсы, и т. д. В отличие от других средств анализа использования в Application Insights, книги позволяют объединить несколько видов визуализаций и анализа, что делает их удобными для такого рода исследований произвольной формы.</span><span class="sxs-lookup"><span data-stu-id="bec3d-108">Exploring hello usage of your app when you don't know hello metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="bec3d-109">О том, как выпущенном функция выполняет команды tooyour, отображение пользователем количество для ключа взаимодействия и другие показатели.</span><span class="sxs-lookup"><span data-stu-id="bec3d-109">Explaining tooyour team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="bec3d-110">Совместное использование результатов hello A / B эксперимента в приложения с другими членами вашей команды.</span><span class="sxs-lookup"><span data-stu-id="bec3d-110">Sharing hello results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="bec3d-111">Можно описать hello цели для hello поэкспериментировать с текстом, а затем Показать все метрики использования и аналитического запроса используется tooevaluate hello эксперимент, вместе с открытым экранными вызовами для выше или ниже целевого каждой метрики, была ли.</span><span class="sxs-lookup"><span data-stu-id="bec3d-111">You can explain hello goals for hello experiment with text, then show each usage metric and Analytics query used tooevaluate hello experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="bec3d-112">Reporting hello влияние сбоя во время использования hello приложение и объединение данных текстовое описание и обсуждение далее шаги tooprevent имеет смысл использовать в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="bec3d-112">Reporting hello impact of an outage on hello usage of your app, combining data, text explanation, and a discussion of next steps tooprevent outages in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="bec3d-113">Ресурс Application Insights должно содержать страницы представлений или пользовательских событий toouse книг.</span><span class="sxs-lookup"><span data-stu-id="bec3d-113">Your Application Insights resource must contain page views or custom events toouse workbooks.</span></span> <span data-ttu-id="bec3d-114">[Узнайте, как tooset веб-страницы toocollect приложения более представления автоматически с помощью пакета SDK Application Insights JavaScript hello](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="bec3d-114">[Learn how tooset up your app toocollect page views automatically with hello Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="bec3d-115">Изменение, переупорядочивание, клонирование и удаление разделов книги</span><span class="sxs-lookup"><span data-stu-id="bec3d-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="bec3d-116">Книга состоит из разделов: отдельно редактируемые визуализации использования, диаграммы, таблицы, текст или результаты запросов аналитики.</span><span class="sxs-lookup"><span data-stu-id="bec3d-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="bec3d-117">tooedit hello содержимое раздела книги, нажмите кнопку hello **изменить** внизу и toohello справа от раздела книги hello.</span><span class="sxs-lookup"><span data-stu-id="bec3d-117">tooedit hello contents of a workbook section, click hello **Edit** button below and toohello right of hello workbook section.</span></span>

![Элементы управления для редактирования статьи книг Application Insights Workbooks](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="bec3d-119">После завершения редактирования раздела, щелкните **сделать редактирования** в hello нижний левый угол раздела hello.</span><span class="sxs-lookup"><span data-stu-id="bec3d-119">When you're done editing a section, click **Done Editing** in hello bottom left corner of hello section.</span></span>

2. <span data-ttu-id="bec3d-120">toocreate дубликат раздел, щелкните hello **клонировать этот раздел** значок.</span><span class="sxs-lookup"><span data-stu-id="bec3d-120">toocreate a duplicate of a section, click hello **Clone this section** icon.</span></span> <span data-ttu-id="bec3d-121">Создание повторяющихся разделов — отлично tooway tooiterate на запросе, не теряя предыдущих итераций.</span><span class="sxs-lookup"><span data-stu-id="bec3d-121">Creating duplicate sections is a great tooway tooiterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="bec3d-122">toomove копию раздела в книге, нажмите кнопку hello **вверх** или **вниз** значок.</span><span class="sxs-lookup"><span data-stu-id="bec3d-122">toomove up a section in a workbook, click hello **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="bec3d-123">tooremove раздел без возможности восстановления, нажмите кнопку hello **удалить** значок.</span><span class="sxs-lookup"><span data-stu-id="bec3d-123">tooremove a section permanently, click hello **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="bec3d-124">Добавление разделов визуализации данных об использовании</span><span class="sxs-lookup"><span data-stu-id="bec3d-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="bec3d-125">Workbooks предлагают четыре типа визуализации аналитики использования,</span><span class="sxs-lookup"><span data-stu-id="bec3d-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="bec3d-126">Каждый ответы на распространенные вопросы по hello использования приложения.</span><span class="sxs-lookup"><span data-stu-id="bec3d-126">Each answers a common question about hello usage of your app.</span></span> <span data-ttu-id="bec3d-127">tooadd таблицах и диаграммах, отличных от эти четыре области, добавьте разделы Analytics запроса (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="bec3d-127">tooadd tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="bec3d-128">tooadd пользователей, сеансы, события или хранения статьи tooyour книги, используйте hello **Добавление пользователей** или других соответствующую кнопку внизу hello hello книги или hello нижней части любого раздела.</span><span class="sxs-lookup"><span data-stu-id="bec3d-128">tooadd a Users, Sessions, Events, or Retention section tooyour workbook, use hello **Add Users** or other corresponding button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

![Раздел "Пользователи" в Workbooks](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="bec3d-130">В разделах **Пользователи** представлены сведения о том, сколько пользователей просмотрели определенную страницу или использовали функцию сайта.</span><span class="sxs-lookup"><span data-stu-id="bec3d-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="bec3d-131">В разделах **Сеансы** представлены сведения о том, сколько сеансов пользователи потратили на просмотр страницы или на использование функций сайта.</span><span class="sxs-lookup"><span data-stu-id="bec3d-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="bec3d-132">В разделах **События** представлены сведения о том, сколько раз пользователи просматривали страницу или использовали функцию сайта.</span><span class="sxs-lookup"><span data-stu-id="bec3d-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="bec3d-133">Каждый из этих типов три раздела предлагает hello одинаковый набор элементов управления и визуализации.</span><span class="sxs-lookup"><span data-stu-id="bec3d-133">Each of these three section types offers hello same sets of controls and visualizations:</span></span>

* <span data-ttu-id="bec3d-134">Дополнительные сведения см. в статье [Анализ пользователей, сеансов и событий в Application Insights](app-insights-usage-segmentation.md).</span><span class="sxs-lookup"><span data-stu-id="bec3d-134">[Learn more about editing Users, Sessions, and Events sections](app-insights-usage-segmentation.md)</span></span>
* <span data-ttu-id="bec3d-135">Переключение hello основной диаграммы, гистограммы сетки, автоматическое аналитики и образец визуализаций пользователей, с помощью hello **Показать диаграммы**, **Показать сетку**, **Показать аналитики**и **Образец эти пользователи** флажки hello верхней части каждого раздела.</span><span class="sxs-lookup"><span data-stu-id="bec3d-135">Toggle hello main chart, histogram grids, automatic insights, and sample users visualizations using hello **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at hello top of each section.</span></span>

![Раздел "Хранение" в Workbooks](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="bec3d-137">В разделах **Хранение** представлены сведения о количестве людей, просматривавших некоторые страницы или использовавших некоторые функции в один день или неделю, которые вернулись в последующий день или неделю.</span><span class="sxs-lookup"><span data-stu-id="bec3d-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* <span data-ttu-id="bec3d-138">Дополнительные сведения см. в статье [Анализ удержания пользователей веб-приложений с помощью Application Insights](app-insights-usage-retention.md).</span><span class="sxs-lookup"><span data-stu-id="bec3d-138">[Learn more about editing Retention sections](app-insights-usage-retention.md)</span></span>
* <span data-ttu-id="bec3d-139">Переключить hello необязательно общего хранения диаграммы с помощью hello **Показать общая диаграмма хранения** флажок hello верхней части раздела hello.</span><span class="sxs-lookup"><span data-stu-id="bec3d-139">Toggle hello optional Overall Retention chart using hello **Show overall retention chart** checkbox at hello top of hello section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="bec3d-140">Добавление разделов аналитики Application Insights</span><span class="sxs-lookup"><span data-stu-id="bec3d-140">Adding Application Insights Analytics sections</span></span>

![Раздел аналитики в Workbooks](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="bec3d-142">использовать tooadd книги tooyour раздел запроса аналитика Analytics приложения hello **добавьте аналитический запрос** кнопку внизу hello hello книги или hello нижней части любого раздела.</span><span class="sxs-lookup"><span data-stu-id="bec3d-142">tooadd an Application Insights Analytics query section tooyour workbook, use hello **Add Analytics query** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

<span data-ttu-id="bec3d-143">Разделы запросов аналитики позволяют добавлять произвольные запросы к данным Application Insights в Workbooks.</span><span class="sxs-lookup"><span data-stu-id="bec3d-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="bec3d-144">Такая гибкость означает, что разделы Analytics запроса должно быть вашей go-toofor ответы на вопросы по веб-узла Кроме hello четырех, перечисленных выше, для пользователей, сеансы, событий и хранения, как:</span><span class="sxs-lookup"><span data-stu-id="bec3d-144">This flexibility means Analytics query sections should be your go-toofor answering any questions about your site other than hello four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="bec3d-145">Исключения, сколько было throw вашего сайта во время hello же период времени как снижением использования?</span><span class="sxs-lookup"><span data-stu-id="bec3d-145">How many exceptions did your site throw during hello same time period as a decline in usage?</span></span>
* <span data-ttu-id="bec3d-146">Была hello распределение времени загрузки страницы для пользователей, просматривающих некоторые страницы?</span><span class="sxs-lookup"><span data-stu-id="bec3d-146">What was hello distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="bec3d-147">Сколько пользователей просматривали конкретные наборы страниц на сайте?</span><span class="sxs-lookup"><span data-stu-id="bec3d-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="bec3d-148">Это может быть полезным toounderstand при наличии группы пользователей, которые используются различные подмножества функциональность веб-узла (использовать hello `join` оператор с hello `kind=leftanti` модификатора hello язык запросов для анализа журналов).</span><span class="sxs-lookup"><span data-stu-id="bec3d-148">This can be useful toounderstand if you have clusters of users who use different subsets of your site's functionality (use hello `join` operator with hello `kind=leftanti` modifier in hello Log Analytics query language).</span></span>

<span data-ttu-id="bec3d-149">Используйте hello [Справочник по языку запросов аналитики журналов](https://docs.loganalytics.io/) toolearn Дополнительные сведения о создании запросов.</span><span class="sxs-lookup"><span data-stu-id="bec3d-149">Use hello [Log Analytics query language reference](https://docs.loganalytics.io/) toolearn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="bec3d-150">Добавление текста и разделы разметки Markdown</span><span class="sxs-lookup"><span data-stu-id="bec3d-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="bec3d-151">Добавление заголовков, описания и комментарии tooyour книги позволяет превратить в речевых набор таблиц и диаграмм.</span><span class="sxs-lookup"><span data-stu-id="bec3d-151">Adding headings, explanations, and commentary tooyour workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="bec3d-152">Текст в книгах колонтитулов hello [синтаксис разметки](https://daringfireball.net/projects/markdown/) для форматирования текста, например заголовки, полужирный, курсив и маркированные списки.</span><span class="sxs-lookup"><span data-stu-id="bec3d-152">Text sections in workbooks support hello [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="bec3d-153">использовать tooadd книгу tooyour раздел текста hello **добавьте текст** кнопку внизу hello hello книги или hello нижней части любого раздела.</span><span class="sxs-lookup"><span data-stu-id="bec3d-153">tooadd a text section tooyour workbook, use hello **Add text** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="bec3d-154">Сохранение и совместное использование книг с коллегами</span><span class="sxs-lookup"><span data-stu-id="bec3d-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="bec3d-155">Книги будут сохраняться в ресурс Application Insights, либо в hello **Мои отчеты** раздел, который является закрытым tooyou или в hello **Общие отчеты** раздел, который является доступного tooeveryone с доступом toohello ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bec3d-155">Workbooks are saved within an Application Insights resource, either in hello **My Reports** section that's private tooyou or in hello **Shared Reports** section that's accessible tooeveryone with access toohello Application Insights resource.</span></span> <span data-ttu-id="bec3d-156">tooview всех книг hello в ресурсе hello щелкните hello **откройте** кнопки действие hello.</span><span class="sxs-lookup"><span data-stu-id="bec3d-156">tooview all hello workbooks in hello resource, click hello **Open** button in hello action bar.</span></span>

<span data-ttu-id="bec3d-157">книги, что сейчас tooshare **Мои отчеты**:</span><span class="sxs-lookup"><span data-stu-id="bec3d-157">tooshare a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="bec3d-158">Нажмите кнопку **откройте** hello панели действий</span><span class="sxs-lookup"><span data-stu-id="bec3d-158">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="bec3d-159">Нажмите кнопку «...» hello рядом с hello книги требуется tooshare</span><span class="sxs-lookup"><span data-stu-id="bec3d-159">Click hello "..." button beside hello workbook you want tooshare</span></span>
3. <span data-ttu-id="bec3d-160">Нажмите кнопку **перемещение отчетов tooShared**.</span><span class="sxs-lookup"><span data-stu-id="bec3d-160">Click **Move tooShared Reports**.</span></span>

<span data-ttu-id="bec3d-161">Щелкните tooshare книги с помощью ссылки или по электронной почте, **общего ресурса** hello панели действий.</span><span class="sxs-lookup"><span data-stu-id="bec3d-161">tooshare a workbook with a link or via email, click **Share** in hello action bar.</span></span> <span data-ttu-id="bec3d-162">Имейте в виду, получатели hello ссылки требуется доступ к toothis ресурсов в книге hello Azure портала tooview hello.</span><span class="sxs-lookup"><span data-stu-id="bec3d-162">Keep in mind that recipients of hello link need access toothis resource in hello Azure portal tooview hello workbook.</span></span> <span data-ttu-id="bec3d-163">изменения toomake, получателям потребуется по крайней мере разрешения участника для ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="bec3d-163">toomake edits, recipients need at least Contributor permissions for hello resource.</span></span>

<span data-ttu-id="bec3d-164">toopin tooan книги tooa ссылку панель мониторинга Azure:</span><span class="sxs-lookup"><span data-stu-id="bec3d-164">toopin a link tooa workbook tooan Azure Dashboard:</span></span>

1. <span data-ttu-id="bec3d-165">Нажмите кнопку **откройте** hello панели действий</span><span class="sxs-lookup"><span data-stu-id="bec3d-165">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="bec3d-166">Нажмите кнопку «...» hello рядом с hello книги требуется toopin</span><span class="sxs-lookup"><span data-stu-id="bec3d-166">Click hello "..." button beside hello workbook you want toopin</span></span>
3. <span data-ttu-id="bec3d-167">Нажмите кнопку **toodashboard ПИН-кода**.</span><span class="sxs-lookup"><span data-stu-id="bec3d-167">Click **Pin toodashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bec3d-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bec3d-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="bec3d-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bec3d-169">Next steps</span></span>
- <span data-ttu-id="bec3d-170">опыт использования tooenable, начать отправку [пользовательские события](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) или [просмотры страниц](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="bec3d-170">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="bec3d-171">При отправке уже, пользовательские события и представления страницы, просмотр hello использования средств toolearn как пользователям использовать эту службу.</span><span class="sxs-lookup"><span data-stu-id="bec3d-171">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="bec3d-172">Пользователи, сеансы, события</span><span class="sxs-lookup"><span data-stu-id="bec3d-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="bec3d-173">Воронки</span><span class="sxs-lookup"><span data-stu-id="bec3d-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="bec3d-174">Сохранение</span><span class="sxs-lookup"><span data-stu-id="bec3d-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="bec3d-175">Средство "Маршруты пользователей"</span><span class="sxs-lookup"><span data-stu-id="bec3d-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="bec3d-176">Добавление контекста пользователей</span><span class="sxs-lookup"><span data-stu-id="bec3d-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
