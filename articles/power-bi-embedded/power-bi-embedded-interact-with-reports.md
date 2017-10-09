---
title: "aaaInteract с отчетами с помощью JavaScript API hello | Документы Microsoft"
description: "Power BI Embedded, взаимодействовать с отчетами с помощью JavaScript API hello"
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
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a><span data-ttu-id="de0f8-103">Взаимодействие с отчетами Power BI, с помощью JavaScript API hello</span><span class="sxs-lookup"><span data-stu-id="de0f8-103">Interact with Power BI reports using hello JavaScript API</span></span>
<span data-ttu-id="de0f8-104">включает Power BI JavaScript API Hello tooeasily можно внедрить Power BI с отчетами в приложения.</span><span class="sxs-lookup"><span data-stu-id="de0f8-104">hello Power BI JavaScript API enables you tooeasily embed Power BI reports into your applications.</span></span> <span data-ttu-id="de0f8-105">С hello API приложений программного взаимодействия с различных отчетов элементы, такие как страницы и фильтры.</span><span class="sxs-lookup"><span data-stu-id="de0f8-105">With hello API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="de0f8-106">Эти интерактивные возможности обеспечивают более полную интеграцию отчетов Power BI с приложениями.</span><span class="sxs-lookup"><span data-stu-id="de0f8-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="de0f8-107">Внедрение отчета Power BI в приложение с помощью iframe, размещенной в рамках приложения hello.</span><span class="sxs-lookup"><span data-stu-id="de0f8-107">You embed a Power BI report in your application by using an iframe that is hosted as part of hello application.</span></span> <span data-ttu-id="de0f8-108">Hello iframe действует как граница между приложением и hello отчета, как видно в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="de0f8-108">hello iframe acts as a boundary between your application and hello report, as you can see in hello following image.</span></span> 

![Плавающий фрейм Power BI Embedded без интерфейса API JavaScript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="de0f8-110">Hello iframe делает hello, внедрение процесса намного проще, но без hello JavaScript API hello отчетов и приложение не может взаимодействовать друг с другом.</span><span class="sxs-lookup"><span data-stu-id="de0f8-110">hello iframe makes hello embedding process a lot easier, but without hello JavaScript API hello report and your application can't interact with each other.</span></span> <span data-ttu-id="de0f8-111">Отсутствие взаимодействия может упростить кажется, что отчет hello не действительно является частью приложения hello.</span><span class="sxs-lookup"><span data-stu-id="de0f8-111">This lack of interaction can make it feel like hello report is not really part of hello application.</span></span> <span data-ttu-id="de0f8-112">Hello отчетов и приложение действительно требуется toocommunicate назад и вперед как hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="de0f8-112">hello report and application really need toocommunicate back and forth, as in hello following image.</span></span>

![Плавающий фрейм Power BI Embedded c интерфейсом API JavaScript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="de0f8-114">Hello Power BI JavaScript API позволяет toowrite кода, можно безопасно передать через границу iframe hello.</span><span class="sxs-lookup"><span data-stu-id="de0f8-114">hello Power BI JavaScript API enables you toowrite code that can securely pass through hello iframe boundary.</span></span> <span data-ttu-id="de0f8-115">Это позволяет tooprogrammatically вашего приложения выполнять действия в отчете и toolisten для событий из действия, настроенные пользователями в отчете hello.</span><span class="sxs-lookup"><span data-stu-id="de0f8-115">This enables your application tooprogrammatically perform an action in a report, and toolisten for events from actions that users make within hello report.</span></span>

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a><span data-ttu-id="de0f8-116">Что можно делать с hello Power BI JavaScript API?</span><span class="sxs-lookup"><span data-stu-id="de0f8-116">What can you do with hello Power BI JavaScript API?</span></span>
<span data-ttu-id="de0f8-117">Hello JavaScript API можно управлять отчетами, перейдите toopages в отчете, фильтрации отчетов и обработки внедрение события.</span><span class="sxs-lookup"><span data-stu-id="de0f8-117">With hello JavaScript API you can manage reports, navigate toopages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="de0f8-118">Hello следующей схеме показана структура hello hello API.</span><span class="sxs-lookup"><span data-stu-id="de0f8-118">hello following diagram shows hello structure of hello API.</span></span>

![Схема интерфейса API JavaScript службы Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="de0f8-120">Управление отчетами</span><span class="sxs-lookup"><span data-stu-id="de0f8-120">Manage reports</span></span>
<span data-ttu-id="de0f8-121">Hello Javascript API позволяет toomanage поведение на уровне отчета и страницы приветствия:</span><span class="sxs-lookup"><span data-stu-id="de0f8-121">hello Javascript API enables you toomanage behavior at hello report and page level:</span></span>

* <span data-ttu-id="de0f8-122">Безопасно внедрение определенный отчет Power BI в приложение — попробуйте hello [внедрить демонстрационного приложения](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="de0f8-122">Embed a specific Power BI Report securely in your application - try hello [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="de0f8-123">Задание маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="de0f8-123">Set access token</span></span>
* <span data-ttu-id="de0f8-124">Настройка отчетов hello</span><span class="sxs-lookup"><span data-stu-id="de0f8-124">Configure hello report</span></span>
  * <span data-ttu-id="de0f8-125">Включение и отключение панели фильтра hello и область навигации по страницам — попробуйте hello [обновить параметры демонстрационного приложения](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="de0f8-125">Enable and disable hello filter pane and page navigation pane - try hello [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="de0f8-126">Настройки по умолчанию для страниц и фильтры - попытайтесь hello [демонстрационный набор значений по умолчанию](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="de0f8-126">Set defaults for pages and filters - try hello [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="de0f8-127">Включение и выключение полноэкранного режима.</span><span class="sxs-lookup"><span data-stu-id="de0f8-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="de0f8-128">Дополнительные сведения о внедрении отчетов.</span><span class="sxs-lookup"><span data-stu-id="de0f8-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a><span data-ttu-id="de0f8-129">Перейдите toopages в отчете</span><span class="sxs-lookup"><span data-stu-id="de0f8-129">Navigate toopages in a report</span></span>
<span data-ttu-id="de0f8-130">Здравствуйте, enbales JavaScript API, вы toodiscover всех страниц в отчете и tooset hello текущей страницы.</span><span class="sxs-lookup"><span data-stu-id="de0f8-130">hello JavaScript API enbales you toodiscover all pages in a report and tooset hello current page.</span></span> <span data-ttu-id="de0f8-131">Повторите hello [навигации демонстрационное приложение](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="de0f8-131">Try hello [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="de0f8-132">Дополнительные сведения о навигации по страницам.</span><span class="sxs-lookup"><span data-stu-id="de0f8-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="de0f8-133">Фильтрация данных в отчете</span><span class="sxs-lookup"><span data-stu-id="de0f8-133">Filter a report</span></span>
<span data-ttu-id="de0f8-134">Hello JavaScript API предоставляет основные и расширенные возможности встроенные отчеты и страницы отчета фильтрации.</span><span class="sxs-lookup"><span data-stu-id="de0f8-134">hello JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="de0f8-135">Повторите hello [фильтрации демонстрационное приложение](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)и просмотрите некоторых вводных кода.</span><span class="sxs-lookup"><span data-stu-id="de0f8-135">Try hello [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="de0f8-136">Базовые фильтры</span><span class="sxs-lookup"><span data-stu-id="de0f8-136">Basic filters</span></span>
<span data-ttu-id="de0f8-137">Базовый фильтр помещается на уровне столбца или иерархии, содержит список значений tooinclude или исключить.</span><span class="sxs-lookup"><span data-stu-id="de0f8-137">A basic filter is placed on a column or hierarchy level and contains a list of values tooinclude or exclude.</span></span>

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


#### <a name="advanced-filters"></a><span data-ttu-id="de0f8-138">Расширенные фильтры</span><span class="sxs-lookup"><span data-stu-id="de0f8-138">Advanced filters</span></span>
<span data-ttu-id="de0f8-139">Расширенные фильтры использовать логический оператор hello и или или и принять одно или два условия, каждый из которых собственные оператор и значение.</span><span class="sxs-lookup"><span data-stu-id="de0f8-139">Advanced filters use hello logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="de0f8-140">Поддерживаются такие условия:</span><span class="sxs-lookup"><span data-stu-id="de0f8-140">Supported conditions are:</span></span>

* <span data-ttu-id="de0f8-141">None</span><span class="sxs-lookup"><span data-stu-id="de0f8-141">None</span></span>
* <span data-ttu-id="de0f8-142">LessThan;</span><span class="sxs-lookup"><span data-stu-id="de0f8-142">LessThan</span></span>
* <span data-ttu-id="de0f8-143">LessThanOrEqual;</span><span class="sxs-lookup"><span data-stu-id="de0f8-143">LessThanOrEqual</span></span>
* <span data-ttu-id="de0f8-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="de0f8-144">GreaterThan</span></span>
* <span data-ttu-id="de0f8-145">GreaterThanOrEqual;</span><span class="sxs-lookup"><span data-stu-id="de0f8-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="de0f8-146">Содержит</span><span class="sxs-lookup"><span data-stu-id="de0f8-146">Contains</span></span>
* <span data-ttu-id="de0f8-147">DoesNotContain;</span><span class="sxs-lookup"><span data-stu-id="de0f8-147">DoesNotContain</span></span>
* <span data-ttu-id="de0f8-148">StartsWith;</span><span class="sxs-lookup"><span data-stu-id="de0f8-148">StartsWith</span></span>
* <span data-ttu-id="de0f8-149">DoesNotStartWith;</span><span class="sxs-lookup"><span data-stu-id="de0f8-149">DoesNotStartWith</span></span>
* <span data-ttu-id="de0f8-150">Is;</span><span class="sxs-lookup"><span data-stu-id="de0f8-150">Is</span></span>
* <span data-ttu-id="de0f8-151">IsNot;</span><span class="sxs-lookup"><span data-stu-id="de0f8-151">IsNot</span></span>
* <span data-ttu-id="de0f8-152">IsBlank;</span><span class="sxs-lookup"><span data-stu-id="de0f8-152">IsBlank</span></span>
* <span data-ttu-id="de0f8-153">IsNotBlank.</span><span class="sxs-lookup"><span data-stu-id="de0f8-153">IsNotBlank</span></span>

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
[<span data-ttu-id="de0f8-154">Дополнительные сведения о фильтрации.</span><span class="sxs-lookup"><span data-stu-id="de0f8-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="de0f8-155">Обработка событий</span><span class="sxs-lookup"><span data-stu-id="de0f8-155">Handling events</span></span>
<span data-ttu-id="de0f8-156">В дополнение к этому toosending информацию в hello iframe, приложения могут также получать сведения о следующих событий, поступающих из hello iframe hello:</span><span class="sxs-lookup"><span data-stu-id="de0f8-156">In addition toosending information into hello iframe, your application can also receive information on hello following events coming from hello iframe:</span></span>

* <span data-ttu-id="de0f8-157">внедрение;</span><span class="sxs-lookup"><span data-stu-id="de0f8-157">Embed</span></span>
  * <span data-ttu-id="de0f8-158">загрузка;</span><span class="sxs-lookup"><span data-stu-id="de0f8-158">loaded</span></span>
  * <span data-ttu-id="de0f8-159">error</span><span class="sxs-lookup"><span data-stu-id="de0f8-159">error</span></span>
* <span data-ttu-id="de0f8-160">Отчеты</span><span class="sxs-lookup"><span data-stu-id="de0f8-160">Reports</span></span>
  * <span data-ttu-id="de0f8-161">изменение страницы;</span><span class="sxs-lookup"><span data-stu-id="de0f8-161">pageChanged</span></span>
  * <span data-ttu-id="de0f8-162">выбор данных (ожидается в ближайшее время).</span><span class="sxs-lookup"><span data-stu-id="de0f8-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="de0f8-163">Дополнительные сведения об обработке событий.</span><span class="sxs-lookup"><span data-stu-id="de0f8-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="de0f8-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de0f8-164">Next steps</span></span>
<span data-ttu-id="de0f8-165">Дополнительные сведения о hello Power BI JavaScript API ознакомьтесь с hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="de0f8-165">For more information about hello Power BI JavaScript API, check out hello following links:</span></span>

* [<span data-ttu-id="de0f8-166">Вики-сайт по интерфейсу API JavaScript</span><span class="sxs-lookup"><span data-stu-id="de0f8-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="de0f8-167">Справочник по объектным моделям</span><span class="sxs-lookup"><span data-stu-id="de0f8-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="de0f8-168">Примеры</span><span class="sxs-lookup"><span data-stu-id="de0f8-168">Samples</span></span>
  * [<span data-ttu-id="de0f8-169">Angular</span><span class="sxs-lookup"><span data-stu-id="de0f8-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="de0f8-170">Ember</span><span class="sxs-lookup"><span data-stu-id="de0f8-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="de0f8-171">Демонстрация в реальном времени</span><span class="sxs-lookup"><span data-stu-id="de0f8-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

