---
title: "Изучение и предоставление общего доступа к данным об использовании c интерактивными книгами Workbooks в Azure Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: 75028b4fbda43d90f56690a33c7eb624fce049c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="80ab4-103">Изучение и предоставление общего доступа к данным об использовании c интерактивными книгами в Application Insights</span><span class="sxs-lookup"><span data-stu-id="80ab4-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="80ab4-104">Workbooks объединяют визуализации данных [Azure Application Insights](app-insights-overview.md), [запросы аналитики](app-insights-analytics.md) и текст в интерактивных документах.</span><span class="sxs-lookup"><span data-stu-id="80ab4-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="80ab4-105">Workbooks могут редактировать другие участники команды с доступом к тому же ресурсу Azure.</span><span class="sxs-lookup"><span data-stu-id="80ab4-105">Workbooks are editable by other team members with access to the same Azure resource.</span></span> <span data-ttu-id="80ab4-106">Это означает, что запросы и элементы управления, используемые для создания книги, будут доступны другим пользователям, читающим книгу, поэтому их легко просматривать, расширять и проверять наличие ошибок.</span><span class="sxs-lookup"><span data-stu-id="80ab4-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span></span>

<span data-ttu-id="80ab4-107">Workbooks полезны для следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="80ab4-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="80ab4-108">Изучение использования приложения, если вам заранее не известны интересующие вас метрики: количество пользователей, коэффициенты хранения, коэффициенты конверсии, и т. д. В отличие от других средств анализа использования в Application Insights, книги позволяют объединить несколько видов визуализаций и анализа, что делает их удобными для такого рода исследований произвольной формы.</span><span class="sxs-lookup"><span data-stu-id="80ab4-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="80ab4-109">Объяснение рабочей группе принципа работы недавно выпущенных компонентов за счет отображения количества ключевых взаимодействий пользователей и других метрик.</span><span class="sxs-lookup"><span data-stu-id="80ab4-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="80ab4-110">Совместное использование результатов альфа и бета-тестирования приложения с другими членами вашей команды.</span><span class="sxs-lookup"><span data-stu-id="80ab4-110">Sharing the results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="80ab4-111">Цели для экспериментов можно объяснить с помощью текста, а затем отобразить каждую метрику использования и аналитический запрос для оценки тестирования вместе с обозначениями того, была ли каждая метрика выше или ниже целевой.</span><span class="sxs-lookup"><span data-stu-id="80ab4-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="80ab4-112">Отчет о влиянии сбоев на использование приложения, объединение данных, текстовое описание и обсуждение следующих шагов, чтобы избежать сбоев в будущем.</span><span class="sxs-lookup"><span data-stu-id="80ab4-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="80ab4-113">Ресурс Application Insights должен содержать просмотры страниц или пользовательские события для использования книг.</span><span class="sxs-lookup"><span data-stu-id="80ab4-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span></span> <span data-ttu-id="80ab4-114">[Узнайте, как настроить приложение для сбора сведений о просмотре страниц автоматически с помощью пакета SDK для JavaScript Application Insights](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="80ab4-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="80ab4-115">Изменение, переупорядочивание, клонирование и удаление разделов книги</span><span class="sxs-lookup"><span data-stu-id="80ab4-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="80ab4-116">Книга состоит из разделов: отдельно редактируемые визуализации использования, диаграммы, таблицы, текст или результаты запросов аналитики.</span><span class="sxs-lookup"><span data-stu-id="80ab4-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="80ab4-117">Чтобы изменить содержимое раздела книги, нажмите кнопку **Изменить** справа под ним.</span><span class="sxs-lookup"><span data-stu-id="80ab4-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span></span>

![Элементы управления для редактирования статьи книг Application Insights Workbooks](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="80ab4-119">Закончив редактирование раздела, щелкните **Done Editing** (Завершить редактирование) в левом нижнем углу раздела.</span><span class="sxs-lookup"><span data-stu-id="80ab4-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span></span>

2. <span data-ttu-id="80ab4-120">Чтобы создать копию раздела, щелкните значок **Clone this section** (Клонировать этот раздел).</span><span class="sxs-lookup"><span data-stu-id="80ab4-120">To create a duplicate of a section, click the **Clone this section** icon.</span></span> <span data-ttu-id="80ab4-121">Создание повторяющихся разделов — это отличный способ для выполнения итерации по запросу без потери предыдущих итераций.</span><span class="sxs-lookup"><span data-stu-id="80ab4-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="80ab4-122">Чтобы перейти к следующему или к предыдущему разделу в книге, щелкните значок **Вверх** или **Вниз**.</span><span class="sxs-lookup"><span data-stu-id="80ab4-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="80ab4-123">Чтобы окончательно удалить раздел, щелкните значок **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="80ab4-123">To remove a section permanently, click the **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="80ab4-124">Добавление разделов визуализации данных об использовании</span><span class="sxs-lookup"><span data-stu-id="80ab4-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="80ab4-125">Workbooks предлагают четыре типа визуализации аналитики использования,</span><span class="sxs-lookup"><span data-stu-id="80ab4-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="80ab4-126">каждый из которых позволяет получить ответы на часто задаваемые вопросы об использовании приложения.</span><span class="sxs-lookup"><span data-stu-id="80ab4-126">Each answers a common question about the usage of your app.</span></span> <span data-ttu-id="80ab4-127">Чтобы добавить таблицы и диаграммы, отличные от этих разделов, добавьте разделы запросов аналитики (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="80ab4-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="80ab4-128">Чтобы добавить разделы "Пользователи", "Сеансы", "События" и "Хранение" в книгу, нажмите кнопку **Добавить пользователей** или другую соответствующую кнопку в нижней части книги или в нижней части любого раздела.</span><span class="sxs-lookup"><span data-stu-id="80ab4-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span></span>

![Раздел "Пользователи" в Workbooks](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="80ab4-130">В разделах **Пользователи** представлены сведения о том, сколько пользователей просмотрели определенную страницу или использовали функцию сайта.</span><span class="sxs-lookup"><span data-stu-id="80ab4-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="80ab4-131">В разделах **Сеансы** представлены сведения о том, сколько сеансов пользователи потратили на просмотр страницы или на использование функций сайта.</span><span class="sxs-lookup"><span data-stu-id="80ab4-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="80ab4-132">В разделах **События** представлены сведения о том, сколько раз пользователи просматривали страницу или использовали функцию сайта.</span><span class="sxs-lookup"><span data-stu-id="80ab4-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="80ab4-133">В каждом из этих трех разделов используются одинаковые элементы управления и визуализации.</span><span class="sxs-lookup"><span data-stu-id="80ab4-133">Each of these three section types offers the same sets of controls and visualizations:</span></span>

* <span data-ttu-id="80ab4-134">Дополнительные сведения см. в статье [Анализ пользователей, сеансов и событий в Application Insights](app-insights-usage-segmentation.md).</span><span class="sxs-lookup"><span data-stu-id="80ab4-134">[Learn more about editing Users, Sessions, and Events sections](app-insights-usage-segmentation.md)</span></span>
* <span data-ttu-id="80ab4-135">Переключить основную диаграмму, сетки гистограммы, автоматическую аналитику и примеры пользовательских визуализаций можно, установив флажки напротив параметров **Show Chart** (Показать диаграмму), **Show Grid** (Показать сетку), **Show Insights** (Показать аналитику) и **Sample of These Users** (Образец этих пользователей) в верхней части каждого раздела.</span><span class="sxs-lookup"><span data-stu-id="80ab4-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span></span>

![Раздел "Хранение" в Workbooks](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="80ab4-137">В разделах **Хранение** представлены сведения о количестве людей, просматривавших некоторые страницы или использовавших некоторые функции в один день или неделю, которые вернулись в последующий день или неделю.</span><span class="sxs-lookup"><span data-stu-id="80ab4-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* <span data-ttu-id="80ab4-138">Дополнительные сведения см. в статье [Анализ удержания пользователей веб-приложений с помощью Application Insights](app-insights-usage-retention.md).</span><span class="sxs-lookup"><span data-stu-id="80ab4-138">[Learn more about editing Retention sections](app-insights-usage-retention.md)</span></span>
* <span data-ttu-id="80ab4-139">Включите общую диаграмму удержания, поставив флажок напротив параметра **Show overall retention chart** (Показать общую диаграмму удержания) в верхней части раздела.</span><span class="sxs-lookup"><span data-stu-id="80ab4-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="80ab4-140">Добавление разделов аналитики Application Insights</span><span class="sxs-lookup"><span data-stu-id="80ab4-140">Adding Application Insights Analytics sections</span></span>

![Раздел аналитики в Workbooks](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="80ab4-142">Чтобы добавить раздел запроса аналитики Application Insights в книгу, используйте кнопку **Добавить запрос аналитики** в нижней части книги, либо в нижней части любого раздела.</span><span class="sxs-lookup"><span data-stu-id="80ab4-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span></span>

<span data-ttu-id="80ab4-143">Разделы запросов аналитики позволяют добавлять произвольные запросы к данным Application Insights в Workbooks.</span><span class="sxs-lookup"><span data-stu-id="80ab4-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="80ab4-144">Такая гибкость означает, что в разделах запросов аналитики будут более точные сведения о вашем сайте, чем в четырех перечисленных выше разделах "Пользователи", "Сеансы", "События" и "Хранение", например:</span><span class="sxs-lookup"><span data-stu-id="80ab4-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="80ab4-145">Сколько исключений об отказе в доступе выдает веб-узел за определенный период времени?</span><span class="sxs-lookup"><span data-stu-id="80ab4-145">How many exceptions did your site throw during the same time period as a decline in usage?</span></span>
* <span data-ttu-id="80ab4-146">Каким было распределение времени загрузки страниц для пользователей, просматривающих определенные страницы?</span><span class="sxs-lookup"><span data-stu-id="80ab4-146">What was the distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="80ab4-147">Сколько пользователей просматривали конкретные наборы страниц на сайте?</span><span class="sxs-lookup"><span data-stu-id="80ab4-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="80ab4-148">Это может быть удобно для определения кластера пользователей, использующих различные подмножества функциональных возможностей веб-сайта (используйте оператор `join` с модификатором `kind=leftanti` на языке запросов Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="80ab4-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span></span>

<span data-ttu-id="80ab4-149">Дополнительные сведения о создании запросов см. в [справочнике по языку запросов Log Analytics](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="80ab4-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="80ab4-150">Добавление текста и разделы разметки Markdown</span><span class="sxs-lookup"><span data-stu-id="80ab4-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="80ab4-151">Добавление заголовков, объяснений и комментариев в Workbooks позволяет превратить набор таблиц и диаграмм в описание.</span><span class="sxs-lookup"><span data-stu-id="80ab4-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="80ab4-152">Разделы текста в книгах поддерживают [синтаксис разметки Markdown](https://daringfireball.net/projects/markdown/) для форматирования текста, например заголовков, полужирного шрифта, курсива и маркированных списков.</span><span class="sxs-lookup"><span data-stu-id="80ab4-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="80ab4-153">Чтобы добавить раздел текста в книгу, используйте кнопку **Добавить текст** в нижней части книги, либо в нижней части любого раздела.</span><span class="sxs-lookup"><span data-stu-id="80ab4-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="80ab4-154">Сохранение и совместное использование книг с коллегами</span><span class="sxs-lookup"><span data-stu-id="80ab4-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="80ab4-155">Книги будут сохраняться в ресурсе Application Insights: в закрытом разделе **Мои отчеты** или в разделе **Общие отчеты**, доступном всем пользователям с доступом к ресурсу Application Insights.</span><span class="sxs-lookup"><span data-stu-id="80ab4-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span></span> <span data-ttu-id="80ab4-156">Для просмотра всех книг в ресурсе нажмите кнопку **Открыть** на панели действий.</span><span class="sxs-lookup"><span data-stu-id="80ab4-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span></span>

<span data-ttu-id="80ab4-157">Чтобы опубликовать книгу, которая находится в разделе **Мои отчеты**, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="80ab4-157">To share a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="80ab4-158">На панели действий щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="80ab4-158">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="80ab4-159">Нажмите кнопку "..." рядом с книгой, к которой необходимо предоставить доступ.</span><span class="sxs-lookup"><span data-stu-id="80ab4-159">Click the "..." button beside the workbook you want to share</span></span>
3. <span data-ttu-id="80ab4-160">Щелкните **Move to Shared Reports** (Переместить в общие отчеты).</span><span class="sxs-lookup"><span data-stu-id="80ab4-160">Click **Move to Shared Reports**.</span></span>

<span data-ttu-id="80ab4-161">Чтобы опубликовать книгу с помощью ссылки или по электронной почте, нажмите кнопку **Поделиться** в области действия.</span><span class="sxs-lookup"><span data-stu-id="80ab4-161">To share a workbook with a link or via email, click **Share** in the action bar.</span></span> <span data-ttu-id="80ab4-162">Имейте в виду, что получателю ссылки потребуется доступ к этому ресурсу на портале Azure, чтобы просмотреть книгу.</span><span class="sxs-lookup"><span data-stu-id="80ab4-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span></span> <span data-ttu-id="80ab4-163">Чтобы внести изменения, получателям потребуется по крайней мере разрешения участника ресурса.</span><span class="sxs-lookup"><span data-stu-id="80ab4-163">To make edits, recipients need at least Contributor permissions for the resource.</span></span>

<span data-ttu-id="80ab4-164">Чтобы закрепить ссылку на книгу на панели мониторинга Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="80ab4-164">To pin a link to a workbook to an Azure Dashboard:</span></span>

1. <span data-ttu-id="80ab4-165">На панели действий щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="80ab4-165">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="80ab4-166">Нажмите кнопку "..." рядом с книгой, которую требуется закрепить.</span><span class="sxs-lookup"><span data-stu-id="80ab4-166">Click the "..." button beside the workbook you want to pin</span></span>
3. <span data-ttu-id="80ab4-167">Щелкните **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="80ab4-167">Click **Pin to dashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80ab4-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80ab4-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="80ab4-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80ab4-169">Next steps</span></span>
- <span data-ttu-id="80ab4-170">Чтобы обеспечить оптимальное использование, начните отправлять [пользовательские события](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) или [сведения о просмотрах страниц](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="80ab4-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="80ab4-171">Если вы уже сделали это, изучите инструменты использования, чтобы узнать, как пользователи используют службу.</span><span class="sxs-lookup"><span data-stu-id="80ab4-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="80ab4-172">Пользователи, сеансы, события</span><span class="sxs-lookup"><span data-stu-id="80ab4-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="80ab4-173">Воронки</span><span class="sxs-lookup"><span data-stu-id="80ab4-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="80ab4-174">Сохранение</span><span class="sxs-lookup"><span data-stu-id="80ab4-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="80ab4-175">Средство "Маршруты пользователей"</span><span class="sxs-lookup"><span data-stu-id="80ab4-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="80ab4-176">Добавление контекста пользователей</span><span class="sxs-lookup"><span data-stu-id="80ab4-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
