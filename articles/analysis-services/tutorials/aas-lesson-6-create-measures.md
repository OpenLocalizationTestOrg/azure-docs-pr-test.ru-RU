---
title: "Учебник по службам Azure Analysis Services: занятие 6 \"Создание мер\" | Документы Майкрософт"
description: "Описывает создание мер в учебном проекте служб Azure Analysis Services."
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
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 90833fa9744eac298b0da82cd3d12f27cc237510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="e9dfd-103">Занятие 6. Создание мер</span><span class="sxs-lookup"><span data-stu-id="e9dfd-103">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="e9dfd-104">В этом занятии вы будете создавать меры для включения в модель.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-104">In this lesson, you create measures to be included in your model.</span></span> <span data-ttu-id="e9dfd-105">Аналогично созданным вами вычисляемым столбцам, мера представляет собой расчет, создаваемый с помощью формулы DAX.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-105">Similar to the calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="e9dfd-106">Но в отличие от вычисляемых столбцов меры вычисляются на основе выбранного пользователем *фильтра*.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-106">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="e9dfd-107">Например, в поле "Метки строк" сводной таблицы добавляется имя определенного столбца или среза.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-107">For example, a particular column or slicer added to the Row Labels field in a PivotTable.</span></span> <span data-ttu-id="e9dfd-108">Значение для каждой ячейки в фильтре вычисляется с учетом применимой меры.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-108">A value for each cell in the filter is then calculated by the applied measure.</span></span> <span data-ttu-id="e9dfd-109">Меры — это эффективные и гибкие средства вычисления, которые пригодятся почти в любых табличных моделях для динамических расчетов с числовыми данными.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-109">Measures are powerful, flexible calculations that you want to include in almost all tabular models to perform dynamic calculations on numerical data.</span></span> <span data-ttu-id="e9dfd-110">Дополнительные сведения см. в статье [Меры](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="e9dfd-110">To learn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="e9dfd-111">Для создания мер используйте *сетку мер*.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-111">To create measures, you use the *Measure Grid*.</span></span> <span data-ttu-id="e9dfd-112">По умолчанию в каждой таблице есть пустая сетка мер. Но меры обычно требуется создавать не для всех таблиц.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-112">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="e9dfd-113">Сетка мер отображается под таблицей в конструкторе моделей при использовании представления данных.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-113">The measure grid appears below a table in the model designer when in Data View.</span></span> <span data-ttu-id="e9dfd-114">Чтобы скрыть или отобразить сетку мер для таблицы, откройте меню **Таблица** и выберите **Показать сетку мер**.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-114">To hide or show the measure grid for a table, click the **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="e9dfd-115">Чтобы создать меру, щелкните пустую ячейку в сетке мер и введите формулу DAX в строке формул.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-115">You can create a measure by clicking an empty cell in the measure grid, and then typing a DAX formula in the formula bar.</span></span> <span data-ttu-id="e9dfd-116">После нажатия клавиши ВВОД для завершения формулы мера появится в ячейке.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-116">When you click ENTER to complete the formula, the measure then appears in the cell.</span></span> <span data-ttu-id="e9dfd-117">Кроме того, можно создать меры с помощью стандартной статистической функции, щелкнув столбец и нажав кнопку "Автосумма" (**∑**) на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-117">You can also create measures using a standard aggregation function by clicking a column, and then clicking the AutoSum button (**∑**) on the toolbar.</span></span> <span data-ttu-id="e9dfd-118">Меры, созданные с помощью функции "Автосумма", появляются в ячейке сетки мер прямо под соответствующим столбцом, но их можно перемещать.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-118">Measures created using the AutoSum feature appear in the measure grid cell directly beneath the column, but can be moved.</span></span>  
  
<span data-ttu-id="e9dfd-119">На этом занятии вы создадите меры путем ввода формулы DAX в строке формул и с помощью функции "Автосумма".</span><span class="sxs-lookup"><span data-stu-id="e9dfd-119">In this lesson, you create measures by both entering a DAX formula in the formula bar, and by using the AutoSum feature.</span></span>  
  
<span data-ttu-id="e9dfd-120">Предполагаемое время выполнения этого занятия: **30 минут**</span><span class="sxs-lookup"><span data-stu-id="e9dfd-120">Estimated time to complete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="e9dfd-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e9dfd-121">Prerequisites</span></span>  
<span data-ttu-id="e9dfd-122">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-122">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="e9dfd-123">Прежде чем выполнять задачи в этом разделе, нужно завершить предыдущее занятие: [Занятие 5. Создание вычисляемых столбцов](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e9dfd-123">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="e9dfd-124">Создание мер</span><span class="sxs-lookup"><span data-stu-id="e9dfd-124">Create measures</span></span>  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a><span data-ttu-id="e9dfd-125">Создание меры DaysCurrentQuarterToDate в таблице DimDate</span><span class="sxs-lookup"><span data-stu-id="e9dfd-125">To create a DaysCurrentQuarterToDate measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="e9dfd-126">В конструкторе моделей щелкните таблицу **DimDate**.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-126">In the model designer, click the **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="e9dfd-127">В сетке мер щелкните верхнюю левую пустую ячейку.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-127">In the measure grid, click the top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="e9dfd-128">В строке формул введите следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="e9dfd-128">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="e9dfd-129">Обратите внимание, что верхняя левая ячейка теперь содержит имя меры **DaysCurrentQuarterToDate** и результат **92**.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-129">Notice the top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by the result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="e9dfd-131">В отличие от вычисляемых столбцов для формул мер можно указать имя меры, затем двоеточие и затем выражение формулы.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-131">Unlike calculated columns, with measure formulas you can type the measure name, followed by a colon, followed by the formula expression.</span></span>

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a><span data-ttu-id="e9dfd-132">Создание меры DaysInCurrentQuarter в таблице DimDate</span><span class="sxs-lookup"><span data-stu-id="e9dfd-132">To create a DaysInCurrentQuarter measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="e9dfd-133">Пока таблица **DimDate** активна в конструкторе моделей, щелкните пустую ячейку под созданной мерой в сетке мер.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-133">With the **DimDate** table still active in the model designer, in the measure grid, click the empty cell below the measure you created.</span></span>  
  
2.  <span data-ttu-id="e9dfd-134">В строке формул введите следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="e9dfd-134">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="e9dfd-135">При создании соотношения для сравнения одного неполного периода и предыдущего периода</span><span class="sxs-lookup"><span data-stu-id="e9dfd-135">When creating a comparison ratio between one incomplete period and the previous period.</span></span> <span data-ttu-id="e9dfd-136">формула должна вычислить пропорцию истекшего периода и сравнить результат с такой же пропорцией предыдущего периода.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-136">The formula must calculate the proportion of the period that has elapsed and compare it to the same proportion in the previous period.</span></span> <span data-ttu-id="e9dfd-137">В этом случае [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] дает пропорцию для текущего периода.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-137">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives the proportion elapsed in the current period.</span></span>  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a><span data-ttu-id="e9dfd-138">Создание меры InternetDistinctCountSalesOrder в таблице FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="e9dfd-138">To create an InternetDistinctCountSalesOrder measure in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="e9dfd-139">Щелкните таблицу **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-139">Click the **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="e9dfd-140">Щелкните заголовок столбца **SalesOrderNumber**.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-140">Click the **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="e9dfd-141">На панели инструментов щелкните стрелку вниз рядом с кнопкой "Автосумма" (**∑**) и выберите **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-141">On the toolbar, click the down-arrow next to the AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="e9dfd-142">Функция "Автосумма" автоматически создает меру для выбранного столбца с помощью стандартной статистической формулы DistinctCount.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-142">The AutoSum feature automatically creates a measure for the selected column using the DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="e9dfd-144">Щелкните новую меру в сетке мер, а затем в поле **Имя меры** окна **Свойства** переименуйте эту меру в **InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-144">In the measure grid, click the new measure, and then in the **Properties** window, in **Measure Name**, rename the measure to **InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a><span data-ttu-id="e9dfd-145">Создание дополнительных мер в таблице FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="e9dfd-145">To create additional measures in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="e9dfd-146">С помощью функции "Автосумма" создайте и назовите следующие меры:</span><span class="sxs-lookup"><span data-stu-id="e9dfd-146">By using the AutoSum feature, create and name the following measures:</span></span>  

    |<span data-ttu-id="e9dfd-147">столбец</span><span class="sxs-lookup"><span data-stu-id="e9dfd-147">Column</span></span>|<span data-ttu-id="e9dfd-148">Имя меры</span><span class="sxs-lookup"><span data-stu-id="e9dfd-148">Measure name</span></span>|<span data-ttu-id="e9dfd-149">Автосумма (∑)</span><span class="sxs-lookup"><span data-stu-id="e9dfd-149">AutoSum (∑)</span></span>|<span data-ttu-id="e9dfd-150">Формула</span><span class="sxs-lookup"><span data-stu-id="e9dfd-150">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="e9dfd-151">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="e9dfd-151">SalesOrderLineNumber</span></span>|<span data-ttu-id="e9dfd-152">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="e9dfd-152">InternetOrderLinesCount</span></span>|<span data-ttu-id="e9dfd-153">Count</span><span class="sxs-lookup"><span data-stu-id="e9dfd-153">Count</span></span>|<span data-ttu-id="e9dfd-154">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="e9dfd-154">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="e9dfd-155">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="e9dfd-155">OrderQuantity</span></span>|<span data-ttu-id="e9dfd-156">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="e9dfd-156">InternetTotalUnits</span></span>|<span data-ttu-id="e9dfd-157">Sum</span><span class="sxs-lookup"><span data-stu-id="e9dfd-157">Sum</span></span>|<span data-ttu-id="e9dfd-158">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="e9dfd-158">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="e9dfd-159">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="e9dfd-159">DiscountAmount</span></span>|<span data-ttu-id="e9dfd-160">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="e9dfd-160">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="e9dfd-161">Sum</span><span class="sxs-lookup"><span data-stu-id="e9dfd-161">Sum</span></span>|<span data-ttu-id="e9dfd-162">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="e9dfd-162">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="e9dfd-163">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="e9dfd-163">TotalProductCost</span></span>|<span data-ttu-id="e9dfd-164">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="e9dfd-164">InternetTotalProductCost</span></span>|<span data-ttu-id="e9dfd-165">Sum</span><span class="sxs-lookup"><span data-stu-id="e9dfd-165">Sum</span></span>|<span data-ttu-id="e9dfd-166">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="e9dfd-166">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="e9dfd-167">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="e9dfd-167">SalesAmount</span></span>|<span data-ttu-id="e9dfd-168">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="e9dfd-168">InternetTotalSales</span></span>|<span data-ttu-id="e9dfd-169">Sum</span><span class="sxs-lookup"><span data-stu-id="e9dfd-169">Sum</span></span>|<span data-ttu-id="e9dfd-170">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="e9dfd-170">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="e9dfd-171">Margin</span><span class="sxs-lookup"><span data-stu-id="e9dfd-171">Margin</span></span>|<span data-ttu-id="e9dfd-172">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="e9dfd-172">InternetTotalMargin</span></span>|<span data-ttu-id="e9dfd-173">Sum</span><span class="sxs-lookup"><span data-stu-id="e9dfd-173">Sum</span></span>|<span data-ttu-id="e9dfd-174">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="e9dfd-174">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="e9dfd-175">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="e9dfd-175">TaxAmt</span></span>|<span data-ttu-id="e9dfd-176">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="e9dfd-176">InternetTotalTaxAmt</span></span>|<span data-ttu-id="e9dfd-177">Sum</span><span class="sxs-lookup"><span data-stu-id="e9dfd-177">Sum</span></span>|<span data-ttu-id="e9dfd-178">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="e9dfd-178">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="e9dfd-179">Freight</span><span class="sxs-lookup"><span data-stu-id="e9dfd-179">Freight</span></span>|<span data-ttu-id="e9dfd-180">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="e9dfd-180">InternetTotalFreight</span></span>|<span data-ttu-id="e9dfd-181">Sum</span><span class="sxs-lookup"><span data-stu-id="e9dfd-181">Sum</span></span>|<span data-ttu-id="e9dfd-182">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="e9dfd-182">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="e9dfd-183">Создайте следующие меры и присвойте им имена в указанном порядке, щелкнув пустую ячейку в сетке мер или используя строку формул:</span><span class="sxs-lookup"><span data-stu-id="e9dfd-183">By clicking an empty cell in the measure grid, and by using the formula bar, create, and name the following measures in order:</span></span>  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
<span data-ttu-id="e9dfd-184">Меры, созданные для таблицы FactInternetSales, можно использовать для анализа критических финансовых данных, таких как продажи, затраты и удельная прибыль, для элементов, определенных с помощью выбранного пользователем фильтра.</span><span class="sxs-lookup"><span data-stu-id="e9dfd-184">Measures created for the FactInternetSales table can be used to analyze critical financial data such as sales, costs, and profit margin for items defined by the user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="e9dfd-185">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="e9dfd-185">What's next?</span></span>
<span data-ttu-id="e9dfd-186">[Занятие 7. Создание ключевых показателей эффективности](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="e9dfd-186">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
