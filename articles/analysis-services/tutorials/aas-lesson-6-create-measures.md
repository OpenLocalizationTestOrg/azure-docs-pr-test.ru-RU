---
<span data-ttu-id="bcffc-101">Заголовок: aaa «занятие учебника Azure Analysis Services 6: создание мер | Документы Microsoft» Описание: описание как toocreate меры в проект tutorial служб Azure Analysis Services hello.</span><span class="sxs-lookup"><span data-stu-id="bcffc-101">title: aaa"Azure Analysis Services tutorial lesson 6: Create measures | Microsoft Docs" description: Describes how toocreate measures in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="bcffc-102">службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''</span><span class="sxs-lookup"><span data-stu-id="bcffc-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="bcffc-103">MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: н/д ms.workload: н/д ms.date: ms.author 06/01/2017 г.: owend</span><span class="sxs-lookup"><span data-stu-id="bcffc-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="bcffc-104">Занятие 6. Создание мер</span><span class="sxs-lookup"><span data-stu-id="bcffc-104">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="bcffc-105">На этом занятии создается toobe меры, включенные в модель.</span><span class="sxs-lookup"><span data-stu-id="bcffc-105">In this lesson, you create measures toobe included in your model.</span></span> <span data-ttu-id="bcffc-106">Аналогичные toohello вычисляемые столбцы, созданные, мера представляет собой вычисление, созданное с помощью формулы DAX.</span><span class="sxs-lookup"><span data-stu-id="bcffc-106">Similar toohello calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="bcffc-107">Но в отличие от вычисляемых столбцов меры вычисляются на основе выбранного пользователем *фильтра*.</span><span class="sxs-lookup"><span data-stu-id="bcffc-107">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="bcffc-108">Например, определенного столбца или среза toohello метки строк поле добавлено в сводной таблице.</span><span class="sxs-lookup"><span data-stu-id="bcffc-108">For example, a particular column or slicer added toohello Row Labels field in a PivotTable.</span></span> <span data-ttu-id="bcffc-109">Значение для каждой ячейки в фильтре hello вычисляется по мере применения hello.</span><span class="sxs-lookup"><span data-stu-id="bcffc-109">A value for each cell in hello filter is then calculated by hello applied measure.</span></span> <span data-ttu-id="bcffc-110">Меры — это мощные гибкие вычисления, которые должны tooinclude в почти все динамические вычисления табличных моделей tooperform с числовыми данными.</span><span class="sxs-lookup"><span data-stu-id="bcffc-110">Measures are powerful, flexible calculations that you want tooinclude in almost all tabular models tooperform dynamic calculations on numerical data.</span></span> <span data-ttu-id="bcffc-111">toolearn более, в разделе [меры](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="bcffc-111">toolearn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="bcffc-112">меры toocreate использовать hello *сетку мер*.</span><span class="sxs-lookup"><span data-stu-id="bcffc-112">toocreate measures, you use hello *Measure Grid*.</span></span> <span data-ttu-id="bcffc-113">По умолчанию в каждой таблице есть пустая сетка мер. Но меры обычно требуется создавать не для всех таблиц.</span><span class="sxs-lookup"><span data-stu-id="bcffc-113">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="bcffc-114">Hello сетка мер появляется внизу таблицы в конструкторе моделей hello в представлении данных.</span><span class="sxs-lookup"><span data-stu-id="bcffc-114">hello measure grid appears below a table in hello model designer when in Data View.</span></span> <span data-ttu-id="bcffc-115">toohide или Показывать сетку мер hello для таблицы, щелкните hello **таблицы** меню, а затем нажмите **Показать сетку мер**.</span><span class="sxs-lookup"><span data-stu-id="bcffc-115">toohide or show hello measure grid for a table, click hello **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="bcffc-116">Можно создать меру, щелкнув пустую ячейку в сетке мер hello и введя DAX-формулы в строке формул hello.</span><span class="sxs-lookup"><span data-stu-id="bcffc-116">You can create a measure by clicking an empty cell in hello measure grid, and then typing a DAX formula in hello formula bar.</span></span> <span data-ttu-id="bcffc-117">Если щелкните toocomplete hello ввод формулы, hello мер, то появится в ячейке hello.</span><span class="sxs-lookup"><span data-stu-id="bcffc-117">When you click ENTER toocomplete hello formula, hello measure then appears in hello cell.</span></span> <span data-ttu-id="bcffc-118">Можно также создать меры, используя стандартную статистическую функцию, щелкнув столбец и выбрав hello кнопки автосуммирования (**∑**) на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="bcffc-118">You can also create measures using a standard aggregation function by clicking a column, and then clicking hello AutoSum button (**∑**) on hello toolbar.</span></span> <span data-ttu-id="bcffc-119">Меры, созданные с помощью функции автосуммирования hello отображается в ячейке сетки мер hello непосредственно под столбцом hello, но могут быть перемещены.</span><span class="sxs-lookup"><span data-stu-id="bcffc-119">Measures created using hello AutoSum feature appear in hello measure grid cell directly beneath hello column, but can be moved.</span></span>  
  
<span data-ttu-id="bcffc-120">На этом занятии вы создаете меры обоих ввода формулы DAX в строке формул hello, а также с помощью функции автосуммирования hello.</span><span class="sxs-lookup"><span data-stu-id="bcffc-120">In this lesson, you create measures by both entering a DAX formula in hello formula bar, and by using hello AutoSum feature.</span></span>  
  
<span data-ttu-id="bcffc-121">Предполагаемое время toocomplete на этом занятии: **30 минут**</span><span class="sxs-lookup"><span data-stu-id="bcffc-121">Estimated time toocomplete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="bcffc-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bcffc-122">Prerequisites</span></span>  
<span data-ttu-id="bcffc-123">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="bcffc-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="bcffc-124">Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятия 5: Создание вычисляемых столбцов](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="bcffc-124">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="bcffc-125">Создание мер</span><span class="sxs-lookup"><span data-stu-id="bcffc-125">Create measures</span></span>  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a><span data-ttu-id="bcffc-126">toocreate DaysCurrentQuarterToDate мера в таблице DimDate hello</span><span class="sxs-lookup"><span data-stu-id="bcffc-126">toocreate a DaysCurrentQuarterToDate measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="bcffc-127">В конструкторе моделей hello щелкните hello **DimDate** таблицы.</span><span class="sxs-lookup"><span data-stu-id="bcffc-127">In hello model designer, click hello **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="bcffc-128">В сетке мер hello щелкните пустую ячейку в левом верхнем hello.</span><span class="sxs-lookup"><span data-stu-id="bcffc-128">In hello measure grid, click hello top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="bcffc-129">В строке формул hello введите следующую формулу hello:</span><span class="sxs-lookup"><span data-stu-id="bcffc-129">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="bcffc-130">Обратите внимание hello верхняя левая ячейка теперь содержит имя меры, **DaysCurrentQuarterToDate**, а затем результат hello **92**.</span><span class="sxs-lookup"><span data-stu-id="bcffc-130">Notice hello top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by hello result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="bcffc-132">В отличие от вычисляемых столбцов причем формулы для мер можно ввести имя меры hello, за которым следует двоеточие, следуют hello выражении формулы.</span><span class="sxs-lookup"><span data-stu-id="bcffc-132">Unlike calculated columns, with measure formulas you can type hello measure name, followed by a colon, followed by hello formula expression.</span></span>

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a><span data-ttu-id="bcffc-133">toocreate DaysInCurrentQuarter мера в таблице DimDate hello</span><span class="sxs-lookup"><span data-stu-id="bcffc-133">toocreate a DaysInCurrentQuarter measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="bcffc-134">С hello **DimDate** таблицы все еще активна в конструкторе моделей hello в сетку мер hello, щелкните пустую ячейку hello ниже созданной мерой hello.</span><span class="sxs-lookup"><span data-stu-id="bcffc-134">With hello **DimDate** table still active in hello model designer, in hello measure grid, click hello empty cell below hello measure you created.</span></span>  
  
2.  <span data-ttu-id="bcffc-135">В строке формул hello введите следующую формулу hello:</span><span class="sxs-lookup"><span data-stu-id="bcffc-135">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="bcffc-136">Во время создания пропорции сравнения между одним неполным периодом и hello предыдущего периода.</span><span class="sxs-lookup"><span data-stu-id="bcffc-136">When creating a comparison ratio between one incomplete period and hello previous period.</span></span> <span data-ttu-id="bcffc-137">Формула Hello необходимо вычислить долю hello hello прошедшего времени периода и сравнивают его toohello же пропорция в hello предыдущего периода.</span><span class="sxs-lookup"><span data-stu-id="bcffc-137">hello formula must calculate hello proportion of hello period that has elapsed and compare it toohello same proportion in hello previous period.</span></span> <span data-ttu-id="bcffc-138">В этом случае [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] дает hello соотношение времени текущего периода в hello.</span><span class="sxs-lookup"><span data-stu-id="bcffc-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives hello proportion elapsed in hello current period.</span></span>  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a><span data-ttu-id="bcffc-139">toocreate InternetDistinctCountSalesOrder мера в таблице FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="bcffc-139">toocreate an InternetDistinctCountSalesOrder measure in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="bcffc-140">Нажмите кнопку hello **FactInternetSales** таблицы.</span><span class="sxs-lookup"><span data-stu-id="bcffc-140">Click hello **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="bcffc-141">Нажмите кнопку hello **SalesOrderNumber** заголовок столбца.</span><span class="sxs-lookup"><span data-stu-id="bcffc-141">Click hello **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="bcffc-142">На панели инструментов hello, нажмите кнопку Далее toohello стрелка вниз hello автосуммирования (**∑**) и затем выберите **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="bcffc-142">On hello toolbar, click hello down-arrow next toohello AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="bcffc-143">Hello автосуммирования автоматически создаст меру для выбранного столбца hello, используя стандартную статистическую формулу DistinctCount hello.</span><span class="sxs-lookup"><span data-stu-id="bcffc-143">hello AutoSum feature automatically creates a measure for hello selected column using hello DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="bcffc-145">В сетке мер hello, щелкните новую меру hello, а затем в hello **свойства** окна в **имя меры**, переименуйте меру hello слишком**InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="bcffc-145">In hello measure grid, click hello new measure, and then in hello **Properties** window, in **Measure Name**, rename hello measure too**InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a><span data-ttu-id="bcffc-146">toocreate дополнительных мер в таблицу FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="bcffc-146">toocreate additional measures in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="bcffc-147">С помощью функции автосуммирования hello, создайте и назовите следующие меры hello.</span><span class="sxs-lookup"><span data-stu-id="bcffc-147">By using hello AutoSum feature, create and name hello following measures:</span></span>  

    |<span data-ttu-id="bcffc-148">столбец</span><span class="sxs-lookup"><span data-stu-id="bcffc-148">Column</span></span>|<span data-ttu-id="bcffc-149">Имя меры</span><span class="sxs-lookup"><span data-stu-id="bcffc-149">Measure name</span></span>|<span data-ttu-id="bcffc-150">Автосумма (∑)</span><span class="sxs-lookup"><span data-stu-id="bcffc-150">AutoSum (∑)</span></span>|<span data-ttu-id="bcffc-151">Формула</span><span class="sxs-lookup"><span data-stu-id="bcffc-151">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="bcffc-152">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="bcffc-152">SalesOrderLineNumber</span></span>|<span data-ttu-id="bcffc-153">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="bcffc-153">InternetOrderLinesCount</span></span>|<span data-ttu-id="bcffc-154">Count</span><span class="sxs-lookup"><span data-stu-id="bcffc-154">Count</span></span>|<span data-ttu-id="bcffc-155">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="bcffc-155">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="bcffc-156">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="bcffc-156">OrderQuantity</span></span>|<span data-ttu-id="bcffc-157">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="bcffc-157">InternetTotalUnits</span></span>|<span data-ttu-id="bcffc-158">Sum</span><span class="sxs-lookup"><span data-stu-id="bcffc-158">Sum</span></span>|<span data-ttu-id="bcffc-159">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="bcffc-159">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="bcffc-160">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="bcffc-160">DiscountAmount</span></span>|<span data-ttu-id="bcffc-161">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="bcffc-161">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="bcffc-162">Sum</span><span class="sxs-lookup"><span data-stu-id="bcffc-162">Sum</span></span>|<span data-ttu-id="bcffc-163">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="bcffc-163">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="bcffc-164">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="bcffc-164">TotalProductCost</span></span>|<span data-ttu-id="bcffc-165">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="bcffc-165">InternetTotalProductCost</span></span>|<span data-ttu-id="bcffc-166">Sum</span><span class="sxs-lookup"><span data-stu-id="bcffc-166">Sum</span></span>|<span data-ttu-id="bcffc-167">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="bcffc-167">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="bcffc-168">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="bcffc-168">SalesAmount</span></span>|<span data-ttu-id="bcffc-169">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="bcffc-169">InternetTotalSales</span></span>|<span data-ttu-id="bcffc-170">Sum</span><span class="sxs-lookup"><span data-stu-id="bcffc-170">Sum</span></span>|<span data-ttu-id="bcffc-171">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="bcffc-171">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="bcffc-172">Margin</span><span class="sxs-lookup"><span data-stu-id="bcffc-172">Margin</span></span>|<span data-ttu-id="bcffc-173">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="bcffc-173">InternetTotalMargin</span></span>|<span data-ttu-id="bcffc-174">Sum</span><span class="sxs-lookup"><span data-stu-id="bcffc-174">Sum</span></span>|<span data-ttu-id="bcffc-175">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="bcffc-175">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="bcffc-176">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="bcffc-176">TaxAmt</span></span>|<span data-ttu-id="bcffc-177">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="bcffc-177">InternetTotalTaxAmt</span></span>|<span data-ttu-id="bcffc-178">Sum</span><span class="sxs-lookup"><span data-stu-id="bcffc-178">Sum</span></span>|<span data-ttu-id="bcffc-179">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="bcffc-179">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="bcffc-180">Freight</span><span class="sxs-lookup"><span data-stu-id="bcffc-180">Freight</span></span>|<span data-ttu-id="bcffc-181">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="bcffc-181">InternetTotalFreight</span></span>|<span data-ttu-id="bcffc-182">Sum</span><span class="sxs-lookup"><span data-stu-id="bcffc-182">Sum</span></span>|<span data-ttu-id="bcffc-183">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="bcffc-183">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="bcffc-184">Щелкнув создайте пустую ячейку в сетке мер hello и с помощью строки формул hello, и hello следующее имя меры в порядке:</span><span class="sxs-lookup"><span data-stu-id="bcffc-184">By clicking an empty cell in hello measure grid, and by using hello formula bar, create, and name hello following measures in order:</span></span>  
  
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
  
<span data-ttu-id="bcffc-185">Меры, созданные для таблицы FactInternetSales hello может быть используется tooanalyze критических финансовых данных, таких как продажи, издержки и маржа прибыли для элементов, которые определены по hello пользователя выбранного фильтра.</span><span class="sxs-lookup"><span data-stu-id="bcffc-185">Measures created for hello FactInternetSales table can be used tooanalyze critical financial data such as sales, costs, and profit margin for items defined by hello user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="bcffc-186">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="bcffc-186">What's next?</span></span>
<span data-ttu-id="bcffc-187">[Занятие 7. Создание ключевых показателей эффективности](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="bcffc-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
