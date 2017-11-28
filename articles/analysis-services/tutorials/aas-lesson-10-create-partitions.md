---
title: "Учебник по службам Azure Analysis Services: занятие 10 \"Создание секций\" | Документы Майкрософт"
description: "Описывает создание секций в учебном проекте служб Azure Analysis Services."
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
ms.openlocfilehash: df74d9cbdcf4916c24955e491767589e72389155
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="36c0b-103">Занятие 10. Создание секций</span><span class="sxs-lookup"><span data-stu-id="36c0b-103">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="36c0b-104">В этом занятии вы создадите секции, чтобы разделить таблицу FactInternetSales на более мелкие логические части, которые можно обрабатывать (обновлять) независимо от других секций.</span><span class="sxs-lookup"><span data-stu-id="36c0b-104">In this lesson, you create partitions to divide the FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="36c0b-105">По умолчанию каждая таблица, включенная в модель, состоит из одной секции, которая содержит все столбцы и строки.</span><span class="sxs-lookup"><span data-stu-id="36c0b-105">By default, every table you include in your model has one partition, which includes all the table’s columns and rows.</span></span> <span data-ttu-id="36c0b-106">Для таблицы FactInternetSales нам нужно разделить данные по годам — по одной секции на каждые пять лет.</span><span class="sxs-lookup"><span data-stu-id="36c0b-106">For the FactInternetSales table, we want to divide the data by year; one partition for each of the table’s five years.</span></span> <span data-ttu-id="36c0b-107">После этого каждую секцию можно будет обрабатывать отдельно.</span><span class="sxs-lookup"><span data-stu-id="36c0b-107">Each partition can then be processed independently.</span></span> <span data-ttu-id="36c0b-108">Дополнительные сведения см. в статье [Секции](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="36c0b-108">To learn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="36c0b-109">Предполагаемое время выполнения этого занятия: **15 минут**</span><span class="sxs-lookup"><span data-stu-id="36c0b-109">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="36c0b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="36c0b-110">Prerequisites</span></span>  
<span data-ttu-id="36c0b-111">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="36c0b-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="36c0b-112">Прежде чем выполнять задачи в этом разделе, нужно завершить предыдущее занятие: [Занятие 9. Создание иерархий](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="36c0b-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="36c0b-113">Создание секций</span><span class="sxs-lookup"><span data-stu-id="36c0b-113">Create partitions</span></span>  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a><span data-ttu-id="36c0b-114">Порядок создания секций в таблице FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="36c0b-114">To create partitions in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="36c0b-115">В обозревателе табличных моделей разверните пункт **Таблицы** и щелкните правой кнопкой мыши **FactInternetSales** > **Секции**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-115">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="36c0b-116">В диспетчере секций щелкните **Копировать**, а затем измените имя на **FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-116">In Partition Manager, click **Copy**, and then change the name to **FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="36c0b-117">Так как секция должна включать только строки за определенный период — 2010 год, нужно изменить выражение запроса.</span><span class="sxs-lookup"><span data-stu-id="36c0b-117">Because you want the partition to include only those rows within a certain period, for the year 2010, you must modify the query expression.</span></span>
  
4.  <span data-ttu-id="36c0b-118">Щелкните **Конструктор**, чтобы открыть редактор запросов, а затем щелкните запрос **FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-118">Click **Design** to open Query Editor, and then click the **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="36c0b-119">В режиме предварительного просмотра щелкните стрелку вниз в заголовке столбца **OrderDate**, а затем выберите **Фильтры даты и времени** > **Между**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-119">In preview, click the down arrow in the **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="36c0b-121">В поле **Показать строки со значением: OrderDate** диалогового окна "Фильтрация строк" оставьте значение **позже или одновременно** и введите в поле даты **1/1/2010**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-121">In the Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in the date field, enter **1/1/2010**.</span></span> <span data-ttu-id="36c0b-122">Оставьте выбранным оператор **И**, выберите **ранее**, введите **1/1/2011** в поле даты и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-122">Leave the **And** operator selected, then select **is before**, then in the date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="36c0b-124">В разделе "Примененные шаги" редактора запросов появится еще один шаг с именем "Строки с примененным фильтром".</span><span class="sxs-lookup"><span data-stu-id="36c0b-124">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="36c0b-125">Этот фильтр позволяет выбрать даты заказов за 2010 год.</span><span class="sxs-lookup"><span data-stu-id="36c0b-125">This filter is to select only order dates from 2010.</span></span>

8.  <span data-ttu-id="36c0b-126">Щелкните **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-126">Click **Import**.</span></span>

    <span data-ttu-id="36c0b-127">В диспетчере секций обратите внимание на то, что теперь выражение запроса имеет дополнительное предложение "Строки с примененным фильтром".</span><span class="sxs-lookup"><span data-stu-id="36c0b-127">In Partition Manager, notice the query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="36c0b-129">Этот оператор указывает, что данная секция должна включать только данные из тех строк, где OrderDate относится к 2010 календарному году, как указано в предложении отфильтрованных строк.</span><span class="sxs-lookup"><span data-stu-id="36c0b-129">This statement specifies this partition should include only the data in those rows where the OrderDate is in the 2010 calendar year as specified in the filtered rows clause.</span></span>  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a><span data-ttu-id="36c0b-130">Порядок создания секции для 2011 года</span><span class="sxs-lookup"><span data-stu-id="36c0b-130">To create a partition for the 2011 year</span></span>  
  
1.  <span data-ttu-id="36c0b-131">В списке секций выберите созданную ранее секцию **FactInternetSales2010**, и щелкните элемент **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-131">In the partitions list, click the **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="36c0b-132">Измените имя секции на **FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-132">Change the partition name to **FactInternetSales2011**.</span></span> 

    <span data-ttu-id="36c0b-133">Для создания предложения отфильтрованных строк не требуется использовать редактор запросов.</span><span class="sxs-lookup"><span data-stu-id="36c0b-133">You do not need to use Query Editor to create a new filtered rows clause.</span></span> <span data-ttu-id="36c0b-134">Так как вы скопировали запрос для 2010 года, достаточно внести в запрос небольшое изменение на 2011 г.</span><span class="sxs-lookup"><span data-stu-id="36c0b-134">Because you created a copy of the query for 2010, all you need to do is make a slight change in the query for 2011.</span></span>
  
2.  <span data-ttu-id="36c0b-135">Чтобы эта секция включала в себя только строки за 2011 год, в поле **Выражение запроса** замените значения года в предложении "Строки с примененным фильтром" на **2011** и **2012**, соответственно. Например:</span><span class="sxs-lookup"><span data-stu-id="36c0b-135">In **Query Expression**, in-order for this partition to include only those rows for the 2011 year, replace the years in the Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="36c0b-136">Порядок создания секций для 2012, 2013 и 2014 годов</span><span class="sxs-lookup"><span data-stu-id="36c0b-136">To create partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="36c0b-137">Выполните описанные выше шаги, создав секции для 2012, 2013 и 2014 годов и изменив значения в предложении "Строки с примененным фильтром", чтобы включить только строки за соответствующий год.</span><span class="sxs-lookup"><span data-stu-id="36c0b-137">Follow the previous steps, creating partitions for 2012, 2013, and 2014, changing the years in the Filtered Rows clause to include only rows for that year.</span></span> 
  

## <a name="delete-the-factinternetsales-partition"></a><span data-ttu-id="36c0b-138">Удаление секции FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="36c0b-138">Delete the FactInternetSales partition</span></span>
<span data-ttu-id="36c0b-139">Теперь, когда у вас есть секции для каждого года, можно удалить секцию FactInternetSales. Это позволяет предотвратить перекрытие при выборе параметра "Обработать все" для обработки секций.</span><span class="sxs-lookup"><span data-stu-id="36c0b-139">Now that you have partitions for each year, you can delete the FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="to-delete-the-factinternetsales-partition"></a><span data-ttu-id="36c0b-140">Порядок удаления секции FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="36c0b-140">To delete the FactInternetSales partition</span></span>
-  <span data-ttu-id="36c0b-141">Щелкните секцию FactInternetSales и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-141">Click the FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="36c0b-142">Обработка секций</span><span class="sxs-lookup"><span data-stu-id="36c0b-142">Process partitions</span></span>  
<span data-ttu-id="36c0b-143">Обратите внимание, что столбец **Последняя обработка** для каждой новой секции в диспетчере секций показывает, что эти секции никогда не обрабатывались.</span><span class="sxs-lookup"><span data-stu-id="36c0b-143">In Partition Manager, notice the **Last Processed** column for each of the new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="36c0b-144">При создании секций следует выполнить операцию "Обработать секции" или "Обработать таблицу" для обновления данных в них.</span><span class="sxs-lookup"><span data-stu-id="36c0b-144">When you create partitions, you should run a Process Partitions or Process Table operation to refresh the data in those partitions.</span></span>  
  
#### <a name="to-process-the-factinternetsales-partitions"></a><span data-ttu-id="36c0b-145">Порядок обработки секций FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="36c0b-145">To process the FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="36c0b-146">Нажмите кнопку **ОК**, диспетчер секций.</span><span class="sxs-lookup"><span data-stu-id="36c0b-146">Click **OK** to close Partition Manager.</span></span>  
  
2.  <span data-ttu-id="36c0b-147">Щелкните таблицу **FactInternetSales**, откройте меню **Модель** и выберите **Обработка** > **Обработать секции**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-147">Click the **FactInternetSales** table, then click the **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="36c0b-148">В диалоговом окне "Обработать секции" установите для параметра **Режим** значение **Обработка по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-148">In the Process Partitions dialog box, verify **Mode** is set to **Process Default**.</span></span>  
  
4.  <span data-ttu-id="36c0b-149">Установите флажок в столбце **Обработка** для каждой из пяти созданных секций, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="36c0b-149">Select the checkbox in the **Process** column for each of the five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="36c0b-151">Если запрашиваются учетные данные олицетворения, введите имя пользователя Windows и пароль, указанные в занятии 2.</span><span class="sxs-lookup"><span data-stu-id="36c0b-151">If you're prompted for Impersonation credentials, enter the Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="36c0b-152">Появляется диалоговое окно **Обработка данных** со сведениями об обработке каждой из секций.</span><span class="sxs-lookup"><span data-stu-id="36c0b-152">The **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="36c0b-153">Обратите внимание, что для каждой секции передается разное количество строк.</span><span class="sxs-lookup"><span data-stu-id="36c0b-153">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="36c0b-154">Каждая секция включает только строки за год, указанный в предложении WHERE инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="36c0b-154">Each partition includes only those rows for the year specified in the WHERE clause in the SQL Statement.</span></span> <span data-ttu-id="36c0b-155">По завершении обработки закройте диалоговое окно "Обработка данных".</span><span class="sxs-lookup"><span data-stu-id="36c0b-155">When processing is finished, go ahead and close the Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="36c0b-157">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="36c0b-157">What's next?</span></span>
<span data-ttu-id="36c0b-158">Перейдите к следующему разделу: [Занятие 11. Создание ролей](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="36c0b-158">Go to the next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
