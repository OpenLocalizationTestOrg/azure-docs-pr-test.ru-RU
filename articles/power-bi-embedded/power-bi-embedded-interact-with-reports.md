---
title: "Взаимодействие с отчетами с помощью интерфейса API JavaScript | Документация Майкрософт"
description: "Power BI Embedded, взаимодействие с отчетами с помощью интерфейса API JavaScript"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 500462ac835674d80650c02aa7fc629b4a975857
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="interact-with-power-bi-reports-using-the-javascript-api"></a><span data-ttu-id="c10a8-103">Взаимодействие с отчетами Power BI с помощью интерфейса API JavaScript</span><span class="sxs-lookup"><span data-stu-id="c10a8-103">Interact with Power BI reports using the JavaScript API</span></span>
<span data-ttu-id="c10a8-104">Интерфейс API JavaScript службы Power BI позволяет с легкостью внедрять отчеты Power BI в приложения.</span><span class="sxs-lookup"><span data-stu-id="c10a8-104">The Power BI JavaScript API enables you to easily embed Power BI reports into your applications.</span></span> <span data-ttu-id="c10a8-105">С помощью API ваши приложения могут программно взаимодействовать с разными элементами отчетов, например со страницами и фильтрами.</span><span class="sxs-lookup"><span data-stu-id="c10a8-105">With the API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="c10a8-106">Эти интерактивные возможности обеспечивают более полную интеграцию отчетов Power BI с приложениями.</span><span class="sxs-lookup"><span data-stu-id="c10a8-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="c10a8-107">Чтобы внедрить отчет Power BI в приложение, воспользуйтесь плавающим фреймом, размещенным как часть приложения.</span><span class="sxs-lookup"><span data-stu-id="c10a8-107">You embed a Power BI report in your application by using an iframe that is hosted as part of the application.</span></span> <span data-ttu-id="c10a8-108">Как показано на рисунке ниже, плавающий фрейм выполняет роль границы между приложением и отчетом.</span><span class="sxs-lookup"><span data-stu-id="c10a8-108">The iframe acts as a boundary between your application and the report, as you can see in the following image.</span></span> 

![Плавающий фрейм Power BI Embedded без интерфейса API JavaScript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="c10a8-110">Плавающий фрейм значительно упрощает внедрение, но без интерфейса API JavaScript отчет и приложение не смогут взаимодействовать друг с другом.</span><span class="sxs-lookup"><span data-stu-id="c10a8-110">The iframe makes the embedding process a lot easier, but without the JavaScript API the report and your application can't interact with each other.</span></span> <span data-ttu-id="c10a8-111">Из-за этого отчет не будет восприниматься как часть приложения.</span><span class="sxs-lookup"><span data-stu-id="c10a8-111">This lack of interaction can make it feel like the report is not really part of the application.</span></span> <span data-ttu-id="c10a8-112">Между отчетом и приложением должен происходить обмен данными (см. рисунок ниже).</span><span class="sxs-lookup"><span data-stu-id="c10a8-112">The report and application really need to communicate back and forth, as in the following image.</span></span>

![Плавающий фрейм Power BI Embedded c интерфейсом API JavaScript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="c10a8-114">Интерфейс API JavaScript службы Power BI позволяет написать код, который может безопасно передаваться через границу плавающего фрейма.</span><span class="sxs-lookup"><span data-stu-id="c10a8-114">The Power BI JavaScript API enables you to write code that can securely pass through the iframe boundary.</span></span> <span data-ttu-id="c10a8-115">Это позволяет приложению программно выполнить действие в отчете и прослушать события, возникающие в результате действий пользователя в отчете.</span><span class="sxs-lookup"><span data-stu-id="c10a8-115">This enables your application to programmatically perform an action in a report, and to listen for events from actions that users make within the report.</span></span>

## <a name="what-can-you-do-with-the-power-bi-javascript-api"></a><span data-ttu-id="c10a8-116">Что можно сделать с помощью интерфейса API JavaScript службы Power BI?</span><span class="sxs-lookup"><span data-stu-id="c10a8-116">What can you do with the Power BI JavaScript API?</span></span>
<span data-ttu-id="c10a8-117">С помощью интерфейса API JavaScript вы можете управлять отчетами, переходить на те или иные страницы отчетов, фильтровать отчеты и управлять событиями внедрения.</span><span class="sxs-lookup"><span data-stu-id="c10a8-117">With the JavaScript API you can manage reports, navigate to pages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="c10a8-118">Структура интерфейса API показана на схеме ниже.</span><span class="sxs-lookup"><span data-stu-id="c10a8-118">The following diagram shows the structure of the API.</span></span>

![Схема интерфейса API JavaScript службы Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="c10a8-120">Управление отчетами</span><span class="sxs-lookup"><span data-stu-id="c10a8-120">Manage reports</span></span>
<span data-ttu-id="c10a8-121">Интерфейс API JavaScript дает возможность управлять поведением на уровне отчета и страницы.</span><span class="sxs-lookup"><span data-stu-id="c10a8-121">The Javascript API enables you to manage behavior at the report and page level:</span></span>

* <span data-ttu-id="c10a8-122">Безопасное внедрение отчетов Power BI в приложение (попробуйте воспользоваться [демонстрационным приложением внедрения](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="c10a8-122">Embed a specific Power BI Report securely in your application - try the [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="c10a8-123">Задание маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="c10a8-123">Set access token</span></span>
* <span data-ttu-id="c10a8-124">Настройка отчета.</span><span class="sxs-lookup"><span data-stu-id="c10a8-124">Configure the report</span></span>
  * <span data-ttu-id="c10a8-125">Включение и отключение панели фильтров и панели навигации по страницам (попробуйте воспользоваться [демонстрационным приложением обновления параметров](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="c10a8-125">Enable and disable the filter pane and page navigation pane - try the [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="c10a8-126">Установка значений по умолчанию для страниц и фильтров (попробуйте воспользоваться [демонстрацией задания значений по умолчанию](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="c10a8-126">Set defaults for pages and filters - try the [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="c10a8-127">Включение и выключение полноэкранного режима.</span><span class="sxs-lookup"><span data-stu-id="c10a8-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="c10a8-128">Дополнительные сведения о внедрении отчетов.</span><span class="sxs-lookup"><span data-stu-id="c10a8-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-to-pages-in-a-report"></a><span data-ttu-id="c10a8-129">Навигация по страницам отчета</span><span class="sxs-lookup"><span data-stu-id="c10a8-129">Navigate to pages in a report</span></span>
<span data-ttu-id="c10a8-130">Интерфейс API JavaScript позволяет обнаруживать все страницы в отчете и задавать текущую страницу.</span><span class="sxs-lookup"><span data-stu-id="c10a8-130">The JavaScript API enbales you to discover all pages in a report and to set the current page.</span></span> <span data-ttu-id="c10a8-131">Попробуйте воспользоваться [демонстрационным приложением навигации](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="c10a8-131">Try the [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="c10a8-132">Дополнительные сведения о навигации по страницам.</span><span class="sxs-lookup"><span data-stu-id="c10a8-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="c10a8-133">Фильтрация данных в отчете</span><span class="sxs-lookup"><span data-stu-id="c10a8-133">Filter a report</span></span>
<span data-ttu-id="c10a8-134">Интерфейс API JavaScript предоставляет базовые и расширенные возможности фильтрации для внедренных отчетов и страниц отчетов.</span><span class="sxs-lookup"><span data-stu-id="c10a8-134">The JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="c10a8-135">Попробуйте [демонстрационное приложение фильтрации](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)и ознакомьтесь с базовым кодом.</span><span class="sxs-lookup"><span data-stu-id="c10a8-135">Try the [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="c10a8-136">Базовые фильтры</span><span class="sxs-lookup"><span data-stu-id="c10a8-136">Basic filters</span></span>
<span data-ttu-id="c10a8-137">Базовый фильтр размещается на уровне столбца или иерархии и содержит ряд значений, которые нужно добавить или исключить.</span><span class="sxs-lookup"><span data-stu-id="c10a8-137">A basic filter is placed on a column or hierarchy level and contains a list of values to include or exclude.</span></span>

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a><span data-ttu-id="c10a8-138">Расширенные фильтры</span><span class="sxs-lookup"><span data-stu-id="c10a8-138">Advanced filters</span></span>
<span data-ttu-id="c10a8-139">Расширенные фильтры используют логические операторы И и ИЛИ и могут принимать одно или два условия, в каждом из которых есть свой оператор и значение.</span><span class="sxs-lookup"><span data-stu-id="c10a8-139">Advanced filters use the logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="c10a8-140">Поддерживаются такие условия:</span><span class="sxs-lookup"><span data-stu-id="c10a8-140">Supported conditions are:</span></span>

* <span data-ttu-id="c10a8-141">None</span><span class="sxs-lookup"><span data-stu-id="c10a8-141">None</span></span>
* <span data-ttu-id="c10a8-142">LessThan;</span><span class="sxs-lookup"><span data-stu-id="c10a8-142">LessThan</span></span>
* <span data-ttu-id="c10a8-143">LessThanOrEqual;</span><span class="sxs-lookup"><span data-stu-id="c10a8-143">LessThanOrEqual</span></span>
* <span data-ttu-id="c10a8-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="c10a8-144">GreaterThan</span></span>
* <span data-ttu-id="c10a8-145">GreaterThanOrEqual;</span><span class="sxs-lookup"><span data-stu-id="c10a8-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="c10a8-146">Содержит</span><span class="sxs-lookup"><span data-stu-id="c10a8-146">Contains</span></span>
* <span data-ttu-id="c10a8-147">DoesNotContain;</span><span class="sxs-lookup"><span data-stu-id="c10a8-147">DoesNotContain</span></span>
* <span data-ttu-id="c10a8-148">StartsWith;</span><span class="sxs-lookup"><span data-stu-id="c10a8-148">StartsWith</span></span>
* <span data-ttu-id="c10a8-149">DoesNotStartWith;</span><span class="sxs-lookup"><span data-stu-id="c10a8-149">DoesNotStartWith</span></span>
* <span data-ttu-id="c10a8-150">Is;</span><span class="sxs-lookup"><span data-stu-id="c10a8-150">Is</span></span>
* <span data-ttu-id="c10a8-151">IsNot;</span><span class="sxs-lookup"><span data-stu-id="c10a8-151">IsNot</span></span>
* <span data-ttu-id="c10a8-152">IsBlank;</span><span class="sxs-lookup"><span data-stu-id="c10a8-152">IsBlank</span></span>
* <span data-ttu-id="c10a8-153">IsNotBlank.</span><span class="sxs-lookup"><span data-stu-id="c10a8-153">IsNotBlank</span></span>

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[<span data-ttu-id="c10a8-154">Дополнительные сведения о фильтрации.</span><span class="sxs-lookup"><span data-stu-id="c10a8-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="c10a8-155">Обработка событий</span><span class="sxs-lookup"><span data-stu-id="c10a8-155">Handling events</span></span>
<span data-ttu-id="c10a8-156">Приложение может не только отправлять информацию в плавающий фрейм, но и получать от него информацию о следующих событиях:</span><span class="sxs-lookup"><span data-stu-id="c10a8-156">In addition to sending information into the iframe, your application can also receive information on the following events coming from the iframe:</span></span>

* <span data-ttu-id="c10a8-157">внедрение;</span><span class="sxs-lookup"><span data-stu-id="c10a8-157">Embed</span></span>
  * <span data-ttu-id="c10a8-158">загрузка;</span><span class="sxs-lookup"><span data-stu-id="c10a8-158">loaded</span></span>
  * <span data-ttu-id="c10a8-159">error</span><span class="sxs-lookup"><span data-stu-id="c10a8-159">error</span></span>
* <span data-ttu-id="c10a8-160">Отчеты</span><span class="sxs-lookup"><span data-stu-id="c10a8-160">Reports</span></span>
  * <span data-ttu-id="c10a8-161">изменение страницы;</span><span class="sxs-lookup"><span data-stu-id="c10a8-161">pageChanged</span></span>
  * <span data-ttu-id="c10a8-162">выбор данных (ожидается в ближайшее время).</span><span class="sxs-lookup"><span data-stu-id="c10a8-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="c10a8-163">Дополнительные сведения об обработке событий.</span><span class="sxs-lookup"><span data-stu-id="c10a8-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="c10a8-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c10a8-164">Next steps</span></span>
<span data-ttu-id="c10a8-165">Дополнительные сведения об интерфейсе API JavaScript службы Power BI доступны по таким ссылкам:</span><span class="sxs-lookup"><span data-stu-id="c10a8-165">For more information about the Power BI JavaScript API, check out the following links:</span></span>

* [<span data-ttu-id="c10a8-166">Вики-сайт по интерфейсу API JavaScript</span><span class="sxs-lookup"><span data-stu-id="c10a8-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="c10a8-167">Справочник по объектным моделям</span><span class="sxs-lookup"><span data-stu-id="c10a8-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="c10a8-168">Примеры</span><span class="sxs-lookup"><span data-stu-id="c10a8-168">Samples</span></span>
  * [<span data-ttu-id="c10a8-169">Angular</span><span class="sxs-lookup"><span data-stu-id="c10a8-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="c10a8-170">Ember</span><span class="sxs-lookup"><span data-stu-id="c10a8-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="c10a8-171">Демонстрация в реальном времени</span><span class="sxs-lookup"><span data-stu-id="c10a8-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

