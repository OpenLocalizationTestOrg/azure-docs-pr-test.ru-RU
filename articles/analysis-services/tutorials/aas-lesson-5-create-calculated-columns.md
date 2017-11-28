---
<span data-ttu-id="71da9-101">Заголовок: aaa» Azure Analysis Services tutorial занятие 5: Создание вычисляемых столбцов | Документы Microsoft» Описание: описание как toocreate вычисляемых столбцов в проект tutorial служб Azure Analysis Services hello.</span><span class="sxs-lookup"><span data-stu-id="71da9-101">title: aaa"Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs" description: Describes how toocreate calculated columns in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="71da9-102">службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''</span><span class="sxs-lookup"><span data-stu-id="71da9-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="71da9-103">MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: н/д ms.workload: н/д ms.date: ms.author 06/01/2017 г.: owend</span><span class="sxs-lookup"><span data-stu-id="71da9-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="71da9-104">Занятие 5. Создание вычисляемых столбцов</span><span class="sxs-lookup"><span data-stu-id="71da9-104">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="71da9-105">В этом занятии вы создадите в модели данные, добавив вычисляемые столбцы.</span><span class="sxs-lookup"><span data-stu-id="71da9-105">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="71da9-106">Можно создать вычисляемые столбцы (как пользовательские столбцы) при использовании получение данных, с помощью hello редактора запросов или более поздней версии в конструкторе like hello модели выполните здесь.</span><span class="sxs-lookup"><span data-stu-id="71da9-106">You can create calculated columns (as custom columns) when using Get Data, by using hello Query Editor, or later in hello model designer like you do here.</span></span> <span data-ttu-id="71da9-107">toolearn более, в разделе [вычисляемых столбцов](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="71da9-107">toolearn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="71da9-108">Вы создадите пять вычисляемых столбцов в трех разных таблицах.</span><span class="sxs-lookup"><span data-stu-id="71da9-108">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="71da9-109">шаги Hello немного отличаются для каждой задачи, показывающей, существует несколько способов toocreate столбцы, переименуйте их и разместить их в различных местах в таблице.</span><span class="sxs-lookup"><span data-stu-id="71da9-109">hello steps are slightly different for each task showing there are several ways toocreate columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="71da9-110">Кроме того, на этом занятии вы впервые воспользуетесь выражениями анализа данных (DAX).</span><span class="sxs-lookup"><span data-stu-id="71da9-110">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="71da9-111">DAX — это специальный язык, позволяющий создавать сложные настраиваемые выражения формул для табличных моделей.</span><span class="sxs-lookup"><span data-stu-id="71da9-111">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="71da9-112">В этом учебнике используется DAX toocreate вычисляемые столбцы, меры и фильтры.</span><span class="sxs-lookup"><span data-stu-id="71da9-112">In this tutorial, you use DAX toocreate calculated columns, measures, and role filters.</span></span> <span data-ttu-id="71da9-113">toolearn более, в разделе [DAX в табличных моделях](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="71da9-113">toolearn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="71da9-114">Предполагаемое время toocomplete на этом занятии: **15 минут**</span><span class="sxs-lookup"><span data-stu-id="71da9-114">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="71da9-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="71da9-115">Prerequisites</span></span>  
<span data-ttu-id="71da9-116">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="71da9-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="71da9-117">Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятия 4: Создание связей](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="71da9-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="71da9-118">Создание вычисляемых столбцов</span><span class="sxs-lookup"><span data-stu-id="71da9-118">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="71da9-119">Создание вычисляемого столбца MonthCalendar таблицы DimDate hello</span><span class="sxs-lookup"><span data-stu-id="71da9-119">Create a MonthCalendar calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="71da9-120">Нажмите кнопку hello **модель** меню > **представление модели** > **представление данных**.</span><span class="sxs-lookup"><span data-stu-id="71da9-120">Click hello **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="71da9-121">Вычисляемые столбцы могут создаваться только с помощью конструктора моделей hello в представлении данных.</span><span class="sxs-lookup"><span data-stu-id="71da9-121">Calculated columns can only be created by using hello model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="71da9-122">В конструкторе моделей hello щелкните hello **DimDate** таблицу (вкладку).</span><span class="sxs-lookup"><span data-stu-id="71da9-122">In hello model designer, click hello **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="71da9-123">Щелкните правой кнопкой мыши hello **CalendarQuarter** заголовок столбца, а затем щелкните **вставить столбец**.</span><span class="sxs-lookup"><span data-stu-id="71da9-123">Right-click hello **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="71da9-124">Новый столбец с именем **вычисляемый столбец 1** — toohello вставленный слева от hello **Календарный квартал** столбца.</span><span class="sxs-lookup"><span data-stu-id="71da9-124">A new column named **Calculated Column 1** is inserted toohello left of hello **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="71da9-125">В hello формул над таблицей hello, введите следующую формулу DAX hello: Автозаполнение помогает ввести hello полные имена столбцов и таблиц и списков hello функций, доступных.</span><span class="sxs-lookup"><span data-stu-id="71da9-125">In hello formula bar above hello table, type hello following DAX formula: AutoComplete helps you type hello fully qualified names of columns and tables, and lists hello functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="71da9-126">Для всех строк hello в вычисляемом столбце hello будут заполнены значениями.</span><span class="sxs-lookup"><span data-stu-id="71da9-126">Values are then populated for all hello rows in hello calculated column.</span></span> <span data-ttu-id="71da9-127">Если прокрутите через таблицу hello видно, что строки могут иметь разные значения для этого столбца на основе данных hello в каждой строке.</span><span class="sxs-lookup"><span data-stu-id="71da9-127">If you scroll down through hello table, you see rows can have different values for this column, based on hello data in each row.</span></span>    
  
5.  <span data-ttu-id="71da9-128">Переименовать этот столбец слишком**MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="71da9-128">Rename this column too**MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="71da9-130">вычисляемый столбец MonthCalendar Hello содержит сортируемое имя для месяца.</span><span class="sxs-lookup"><span data-stu-id="71da9-130">hello MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="71da9-131">Создание вычисляемого столбца DayOfWeek таблицы DimDate hello</span><span class="sxs-lookup"><span data-stu-id="71da9-131">Create a DayOfWeek calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="71da9-132">С hello **DimDate** активной таблице, нажмите кнопку hello **столбца** меню, а затем нажмите **добавить столбец**.</span><span class="sxs-lookup"><span data-stu-id="71da9-132">With hello **DimDate** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="71da9-133">В строке формул hello введите следующую формулу hello:</span><span class="sxs-lookup"><span data-stu-id="71da9-133">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="71da9-134">Завершив построение формулы hello, нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="71da9-134">When you've finished building hello formula, press ENTER.</span></span> <span data-ttu-id="71da9-135">toohello правого края hello таблицу добавляется новый столбец Hello.</span><span class="sxs-lookup"><span data-stu-id="71da9-135">hello new column is added toohello far right of hello table.</span></span>  
  
3.  <span data-ttu-id="71da9-136">Переименовать столбец hello слишком**DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="71da9-136">Rename hello column too**DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="71da9-137">Щелкните заголовок столбца hello, а затем перетащите столбец hello между hello **EnglishDayNameOfWeek** столбец и hello **DayNumberOfMonth** столбца.</span><span class="sxs-lookup"><span data-stu-id="71da9-137">Click hello column heading, and then drag hello column between hello **EnglishDayNameOfWeek** column and hello **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="71da9-138">Перемещение столбцов в таблице позволяет упростить toonavigate.</span><span class="sxs-lookup"><span data-stu-id="71da9-138">Moving columns in your table makes it easier toonavigate.</span></span>  
  
<span data-ttu-id="71da9-139">вычисляемый столбец DayOfWeek Hello содержит сортируемое имя дня недели hello.</span><span class="sxs-lookup"><span data-stu-id="71da9-139">hello DayOfWeek calculated column provides a sortable name for hello day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="71da9-140">Создание вычисляемого столбца ProductSubcategoryName в таблице DimProduct hello</span><span class="sxs-lookup"><span data-stu-id="71da9-140">Create a ProductSubcategoryName calculated column in hello DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="71da9-141">В hello **DimProduct** таблица, прокрутите toohello правому краю таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="71da9-141">In hello **DimProduct** table, scroll toohello far right of hello table.</span></span> <span data-ttu-id="71da9-142">Обратите внимание hello самый правый столбец называется **добавить столбец** (курсивом), щелкните заголовок столбца hello.</span><span class="sxs-lookup"><span data-stu-id="71da9-142">Notice hello right-most column is named **Add Column** (italicized), click hello column heading.</span></span>  
  
2.  <span data-ttu-id="71da9-143">В строке формул hello введите следующую формулу hello:</span><span class="sxs-lookup"><span data-stu-id="71da9-143">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="71da9-144">Переименовать столбец hello слишком**ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="71da9-144">Rename hello column too**ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="71da9-145">вычисляемый столбец Hello ProductSubcategoryName — используется toocreate иерархии в таблице DimProduct hello, которое включает данные из столбца EnglishProductSubcategoryName hello в таблице DimProductSubcategory hello.</span><span class="sxs-lookup"><span data-stu-id="71da9-145">hello ProductSubcategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductSubcategoryName column in hello DimProductSubcategory table.</span></span> <span data-ttu-id="71da9-146">Иерархии не могут охватывать более одной таблицы.</span><span class="sxs-lookup"><span data-stu-id="71da9-146">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="71da9-147">Вы создадите иерархии позднее в занятии 9.</span><span class="sxs-lookup"><span data-stu-id="71da9-147">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="71da9-148">Создание вычисляемого столбца ProductCategoryName в таблице DimProduct hello</span><span class="sxs-lookup"><span data-stu-id="71da9-148">Create a ProductCategoryName calculated column in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="71da9-149">С hello **DimProduct** активной таблице, нажмите кнопку hello **столбца** меню, а затем нажмите **добавить столбец**.</span><span class="sxs-lookup"><span data-stu-id="71da9-149">With hello **DimProduct** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="71da9-150">В строке формул hello введите следующую формулу hello:</span><span class="sxs-lookup"><span data-stu-id="71da9-150">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="71da9-151">Переименовать столбец hello слишком**ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="71da9-151">Rename hello column too**ProductCategoryName**.</span></span>  
  
<span data-ttu-id="71da9-152">вычисляемый столбец ProductCategoryName Hello — используется toocreate иерархии в таблице DimProduct hello, которое включает данные из столбца EnglishProductCategoryName hello в таблице DimProductCategory hello.</span><span class="sxs-lookup"><span data-stu-id="71da9-152">hello ProductCategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductCategoryName column in hello DimProductCategory table.</span></span> <span data-ttu-id="71da9-153">Иерархии не могут охватывать более одной таблицы.</span><span class="sxs-lookup"><span data-stu-id="71da9-153">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a><span data-ttu-id="71da9-154">Создание вычисляемого столбца поля таблицы FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="71da9-154">Create a Margin calculated column in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="71da9-155">Выберите в конструкторе моделей hello hello **FactInternetSales** таблицы.</span><span class="sxs-lookup"><span data-stu-id="71da9-155">In hello model designer, select hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="71da9-156">Создать новый вычисляемый столбец между hello **SalesAmount** столбец и hello **TaxAmt** столбца.</span><span class="sxs-lookup"><span data-stu-id="71da9-156">Create a new calculated column between hello **SalesAmount** column and hello **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="71da9-157">В строке формул hello введите следующую формулу hello:</span><span class="sxs-lookup"><span data-stu-id="71da9-157">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="71da9-158">Переименовать столбец hello слишком**поля**.</span><span class="sxs-lookup"><span data-stu-id="71da9-158">Rename hello column too**Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="71da9-160">вычисляемый столбец Hello поля — используется tooanalyze прибыли для каждой продажи.</span><span class="sxs-lookup"><span data-stu-id="71da9-160">hello Margin calculated column is used tooanalyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="71da9-161">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="71da9-161">What's next?</span></span>
<span data-ttu-id="71da9-162">[Занятие 6. Создание мер](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="71da9-162">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
