---
title: "Дополнительное занятие для учебника по службам Azure Analysis Services: \"Строки детализации\" | Документы Майкрософт"
description: "Описывает, как создать выражение строк детализации в учебном проекте служб Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: fde5cd9a9efc3a13e731a91962ced5c086a72355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="ce003-103">Дополнительное занятие. Строки детализации</span><span class="sxs-lookup"><span data-stu-id="ce003-103">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="ce003-104">В этом дополнительном занятии вы воспользуетесь редактором DAX для определения пользовательского выражения строк детализации.</span><span class="sxs-lookup"><span data-stu-id="ce003-104">In this supplemental lesson, you use the DAX Editor to define a custom Detail Rows Expression.</span></span> <span data-ttu-id="ce003-105">Выражение строк детализации — это свойство меры, предоставляющее конечным пользователям дополнительные сведения об агрегированных результатах для меры.</span><span class="sxs-lookup"><span data-stu-id="ce003-105">A Detail Rows Expression is a property on a measure, providing end-users more information about the aggregated results of a measure.</span></span> 
  
<span data-ttu-id="ce003-106">Предполагаемое время выполнения этого занятия: **10 минут**</span><span class="sxs-lookup"><span data-stu-id="ce003-106">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ce003-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ce003-107">Prerequisites</span></span>  
<span data-ttu-id="ce003-108">Это дополнительное занятие входит в учебник по табличному моделированию.</span><span class="sxs-lookup"><span data-stu-id="ce003-108">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="ce003-109">Прежде чем выполнять задачи из этого дополнительного занятия, следует завершить все предыдущие занятия или располагать готовым учебным проектом модели интернет-продаж Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="ce003-109">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-to-solve"></a><span data-ttu-id="ce003-110">Какие задачи нам нужно решить?</span><span class="sxs-lookup"><span data-stu-id="ce003-110">What do we need to solve?</span></span>
<span data-ttu-id="ce003-111">Прежде чем добавлять выражение строк детализации, давайте взглянем на сведения о мере InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="ce003-111">Let's look at the details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="ce003-112">В SSDT откройте меню **Модель** и выберите **Анализ в Excel**, чтобы открыть Excel и создать пустую сводную таблицу.</span><span class="sxs-lookup"><span data-stu-id="ce003-112">In SSDT, click the **Model** menu > **Analyze in Excel** to open Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="ce003-113">В области **Поля сводной таблицы** добавьте меру **InternetTotalSales** из таблицы FactInternetSales поле **Значения**, **CalendarYear** из таблицы DimDate поле **Столбцы** и **EnglishCountryRegionName** в поле **Строки**.</span><span class="sxs-lookup"><span data-stu-id="ce003-113">In **PivotTable Fields**, add the **InternetTotalSales** measure from the FactInternetSales table to **Values**, **CalendarYear** from the DimDate table to **Columns**, and **EnglishCountryRegionName** to **Rows**.</span></span> <span data-ttu-id="ce003-114">Теперь наша сводная таблица предоставляет агрегированные результаты из меры InternetTotalSales по регионам и годам.</span><span class="sxs-lookup"><span data-stu-id="ce003-114">Our PivotTable now gives us aggregated results from the InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="ce003-116">В сводной таблице дважды щелкните агрегированное значение для года и имени региона.</span><span class="sxs-lookup"><span data-stu-id="ce003-116">In the PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="ce003-117">Здесь мы выбрали значение для Австралии за 2014 год.</span><span class="sxs-lookup"><span data-stu-id="ce003-117">Here we double-clicked the value for Australia and the year 2014.</span></span> <span data-ttu-id="ce003-118">Открывается новый лист с данными, но это не те данные, которые нам требуются.</span><span class="sxs-lookup"><span data-stu-id="ce003-118">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="ce003-120">Здесь нам бы хотелось увидеть таблицу со столбцами и строками данных, имеющих отношение к агрегированному результату нашей меры InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="ce003-120">What we would like to see here is a table containing columns and rows of data that contribute to the aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="ce003-121">Для этого можно добавить выражение строк детализации в качестве свойства меры.</span><span class="sxs-lookup"><span data-stu-id="ce003-121">To do that, we can add a Detail Rows Expression as a property of the measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="ce003-122">Добавление выражения строк детализации</span><span class="sxs-lookup"><span data-stu-id="ce003-122">Add a Detail Rows Expression</span></span>

#### <a name="to-create-a-detail-rows-expression"></a><span data-ttu-id="ce003-123">Чтобы добавить выражение строк детализации, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ce003-123">To create a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="ce003-124">В сетке мер таблицы FactInternetSales SSDT выберите меру **InternetTotalSales**.</span><span class="sxs-lookup"><span data-stu-id="ce003-124">In SSDT, in the FactInternetSales table's measure grid, click the **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="ce003-125">В области **Свойства** > **Выражение строк детализации** нажмите кнопку редактора, чтобы открыть редактор DAX.</span><span class="sxs-lookup"><span data-stu-id="ce003-125">In **Properties** > **Detail Rows Expression**, click the editor button to open the DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="ce003-127">В редакторе DAX введите следующее выражение:</span><span class="sxs-lookup"><span data-stu-id="ce003-127">In DAX Editor, enter the following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="ce003-128">Это выражение указывает имена, столбцы и результаты мер из таблицы FactInternetSales. Когда пользователь дважды щелкает агрегированный результат в сводной таблице или отчете, открываются связанные таблицы.</span><span class="sxs-lookup"><span data-stu-id="ce003-128">This expression specifies names, columns, and measure results from the FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="ce003-129">Вернитесь в Excel, удалите лист, созданный в шаге 3, а затем дважды щелкните агрегированное значение.</span><span class="sxs-lookup"><span data-stu-id="ce003-129">Back in Excel, delete the sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="ce003-130">На этот раз с помощью определенного для меры свойства "Выражение строк детализации" открывается новый лист, содержащий гораздо больше полезных данных.</span><span class="sxs-lookup"><span data-stu-id="ce003-130">This time, with a Detail Rows Expression property defined for the measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="ce003-132">Разверните модель заново.</span><span class="sxs-lookup"><span data-stu-id="ce003-132">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="ce003-133">См. также</span><span class="sxs-lookup"><span data-stu-id="ce003-133">See Also</span></span>  
<span data-ttu-id="ce003-134">[Функция SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="ce003-134">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="ce003-135">Дополнительное занятие. Динамическая безопасность</span><span class="sxs-lookup"><span data-stu-id="ce003-135">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="ce003-136">Дополнительное занятие. Неоднородные иерархии</span><span class="sxs-lookup"><span data-stu-id="ce003-136">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
