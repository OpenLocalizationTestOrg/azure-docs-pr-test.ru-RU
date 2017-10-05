---
title: "Учебник по службам Azure Analysis Services: занятие 5 \"Создание вычисляемых столбцов\" | Документы Майкрософт"
description: "Описывает создание вычисляемых столбцов в учебном проекте служб Azure Analysis Services."
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
ms.openlocfilehash: 893371145d77e156843271907aeef0c3756d0403
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="ad5a9-103">Занятие 5. Создание вычисляемых столбцов</span><span class="sxs-lookup"><span data-stu-id="ad5a9-103">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="ad5a9-104">В этом занятии вы создадите в модели данные, добавив вычисляемые столбцы.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-104">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="ad5a9-105">Вычисляемые столбцы можно создать (в качестве настраиваемых столбцов) при использовании функции получения данных, с помощью редактора запросов или позднее в конструкторе моделей. Последним способом вы и воспользуетесь.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-105">You can create calculated columns (as custom columns) when using Get Data, by using the Query Editor, or later in the model designer like you do here.</span></span> <span data-ttu-id="ad5a9-106">Дополнительные сведения см. в разделе [Вычисляемые столбцы](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="ad5a9-106">To learn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="ad5a9-107">Вы создадите пять вычисляемых столбцов в трех разных таблицах.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-107">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="ad5a9-108">Шаги для каждой задачи немного отличаются, что позволяет продемонстрировать несколько способов создания и переименования столбцов, а также их перемещения в таблице.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-108">The steps are slightly different for each task showing there are several ways to create columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="ad5a9-109">Кроме того, на этом занятии вы впервые воспользуетесь выражениями анализа данных (DAX).</span><span class="sxs-lookup"><span data-stu-id="ad5a9-109">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="ad5a9-110">DAX — это специальный язык, позволяющий создавать сложные настраиваемые выражения формул для табличных моделей.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-110">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="ad5a9-111">В этом руководстве вы будете использовать DAX для создания вычисляемых столбцов, мер и фильтров ролей.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-111">In this tutorial, you use DAX to create calculated columns, measures, and role filters.</span></span> <span data-ttu-id="ad5a9-112">Дополнительные сведения см. в разделе [DAX в табличных моделях](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="ad5a9-112">To learn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="ad5a9-113">Предполагаемое время выполнения этого занятия: **15 минут**</span><span class="sxs-lookup"><span data-stu-id="ad5a9-113">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ad5a9-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ad5a9-114">Prerequisites</span></span>  
<span data-ttu-id="ad5a9-115">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-115">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="ad5a9-116">Прежде чем выполнять задачи в этом разделе, нужно завершить предыдущее занятие: [Занятие 4. Создание связей](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="ad5a9-116">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="ad5a9-117">Создание вычисляемых столбцов</span><span class="sxs-lookup"><span data-stu-id="ad5a9-117">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="ad5a9-118">Создание вычисляемого столбца MonthCalendar в таблице DimDate</span><span class="sxs-lookup"><span data-stu-id="ad5a9-118">Create a MonthCalendar calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="ad5a9-119">Щелкните меню **Модель** и выберите **Представление модели** > **Представление данных**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-119">Click the **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="ad5a9-120">Вычисляемые столбцы можно создать только с помощью конструктора моделей в представлении данных.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-120">Calculated columns can only be created by using the model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="ad5a9-121">В конструкторе моделей щелкните таблицу **DimDate** (вкладка).</span><span class="sxs-lookup"><span data-stu-id="ad5a9-121">In the model designer, click the **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="ad5a9-122">Щелкните правой кнопкой мыши заголовок столбца **CalendarQuarter** и выберите пункт **Вставить столбец**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-122">Right-click the **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="ad5a9-123">Новый столбец с именем **Вычисляемый столбец 1** вставляется слева от столбца **Календарный квартал**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-123">A new column named **Calculated Column 1** is inserted to the left of the **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="ad5a9-124">В строке формул над таблицей введите приведенную ниже формулу DAX. Компонент автозаполнения помогает вводить полные имена столбцов и таблиц и выводит список доступных функций.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-124">In the formula bar above the table, type the following DAX formula: AutoComplete helps you type the fully qualified names of columns and tables, and lists the functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="ad5a9-125">После этого все строки в вычисляемом столбце заполняются значениями.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-125">Values are then populated for all the rows in the calculated column.</span></span> <span data-ttu-id="ad5a9-126">Если прокрутить содержимое таблицы вниз, вы увидите, что строки могут содержать разные значения для этого столбца, в зависимости от данных в каждой строке.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-126">If you scroll down through the table, you see rows can have different values for this column, based on the data in each row.</span></span>    
  
5.  <span data-ttu-id="ad5a9-127">Переименуйте этот столбец в **MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-127">Rename this column to **MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="ad5a9-129">Вычисляемый столбец MonthCalendar содержит поддерживающее сортировку имя для месяца.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-129">The MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="ad5a9-130">Создание вычисляемого столбца DayOfWeek в таблице DimDate</span><span class="sxs-lookup"><span data-stu-id="ad5a9-130">Create a DayOfWeek calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="ad5a9-131">Пока таблица **DimDate** активна, откройте меню **Столбец** и выберите **Добавить столбец**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-131">With the **DimDate** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="ad5a9-132">В строке формул введите следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="ad5a9-132">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="ad5a9-133">Завершив составление формулы, нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-133">When you've finished building the formula, press ENTER.</span></span> <span data-ttu-id="ad5a9-134">С правого края таблицы добавляется новый столбец.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-134">The new column is added to the far right of the table.</span></span>  
  
3.  <span data-ttu-id="ad5a9-135">Переименуйте его в **DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-135">Rename the column to **DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="ad5a9-136">Щелкните заголовок столбца и перетащите его на место между столбцами **EnglishDayNameOfWeek** и **DayNumberOfMonth**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-136">Click the column heading, and then drag the column between the **EnglishDayNameOfWeek** column and the **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="ad5a9-137">Перемещение столбцов в таблице облегчает навигацию.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-137">Moving columns in your table makes it easier to navigate.</span></span>  
  
<span data-ttu-id="ad5a9-138">Вычисляемый столбец DayOfWeek содержит поддерживающее сортировку имя для дня недели.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-138">The DayOfWeek calculated column provides a sortable name for the day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="ad5a9-139">Создание вычисляемого столбца ProductSubcategoryName в таблице DimProduct</span><span class="sxs-lookup"><span data-stu-id="ad5a9-139">Create a ProductSubcategoryName calculated column in the DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="ad5a9-140">Прокрутите таблицу **DimProduct** до правого края.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-140">In the **DimProduct** table, scroll to the far right of the table.</span></span> <span data-ttu-id="ad5a9-141">Найдите крайний правый столбец с именем **Добавить столбец** (курсивом) и щелкните его заголовок.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-141">Notice the right-most column is named **Add Column** (italicized), click the column heading.</span></span>  
  
2.  <span data-ttu-id="ad5a9-142">В строке формул введите следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="ad5a9-142">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="ad5a9-143">Переименуйте столбец в **ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-143">Rename the column to **ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="ad5a9-144">Вычисляемый столбец ProductSubcategoryName используется для создания иерархии в таблице DimProduct, которая включает данные из столбца EnglishProductSubcategoryName таблицы DimProductSubcategory.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-144">The ProductSubcategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductSubcategoryName column in the DimProductSubcategory table.</span></span> <span data-ttu-id="ad5a9-145">Иерархии не могут охватывать более одной таблицы.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-145">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="ad5a9-146">Вы создадите иерархии позднее в занятии 9.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-146">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="ad5a9-147">Создание вычисляемого столбца ProductCategoryName в таблице DimProduct</span><span class="sxs-lookup"><span data-stu-id="ad5a9-147">Create a ProductCategoryName calculated column in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="ad5a9-148">Пока таблица **DimProduct** активна, откройте меню **Столбец** и выберите элемент **Добавить столбец**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-148">With the **DimProduct** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="ad5a9-149">В строке формул введите следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="ad5a9-149">In the formula bar, type the following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="ad5a9-150">Переименуйте столбец в **ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-150">Rename the column to **ProductCategoryName**.</span></span>  
  
<span data-ttu-id="ad5a9-151">Вычисляемый столбец ProductCategoryName используется для создания иерархии в таблице DimProduct, которая включает данные из столбца EnglishProductCategoryName таблицы DimProductCategory.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-151">The ProductCategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductCategoryName column in the DimProductCategory table.</span></span> <span data-ttu-id="ad5a9-152">Иерархии не могут охватывать более одной таблицы.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-152">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a><span data-ttu-id="ad5a9-153">Создание вычисляемого столбца Margin в таблице FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="ad5a9-153">Create a Margin calculated column in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="ad5a9-154">В конструкторе моделей выберите таблицу **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-154">In the model designer, select the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="ad5a9-155">Создайте вычисляемый столбец между столбцами **SalesAmount** и **TaxAmt**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-155">Create a new calculated column between the **SalesAmount** column and the **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="ad5a9-156">В строке формул введите следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="ad5a9-156">In the formula bar, type the following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="ad5a9-157">Переименуйте столбец в **Margin**.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-157">Rename the column to **Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="ad5a9-159">Вычисляемый столбец Margin используется при анализе рентабельности для каждой продажи.</span><span class="sxs-lookup"><span data-stu-id="ad5a9-159">The Margin calculated column is used to analyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="ad5a9-160">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="ad5a9-160">What's next?</span></span>
<span data-ttu-id="ad5a9-161">[Занятие 6. Создание мер](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="ad5a9-161">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
